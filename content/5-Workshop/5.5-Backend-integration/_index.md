---
title: "NestJS Backend Integration"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### NestJS Backend Integration, REST APIs, Amazon S3 Upload & Security Guards

In this section, we examine how the NestJS backend implements **REST APIs**, integrates the **Amazon Cognito SDK**, verifies cryptographic **RSA JWT signatures (`us-east-1`)**, and handles image file uploads to **Amazon S3**.

#### 1. Start Backend Server & Verify REST APIs

Start the local backend server (NestJS) to verify the API connectivity:
```bash
cd backend
npm run start:dev
```
Then, access the public Business Discovery API at `http://localhost:3000/businesses`. You will see a JSON response containing the list of public businesses fetched from your database.

![REST API JSON Response](/images/5-Workshop/5.5-Backend-integration/swagger.png)

#### 2. Implemented & Protected REST APIs

- **Businesses (`BusinessesController`)**:
  - `POST /businesses`: Create new Business (Requires `JwtAuthGuard`).
  - `GET /businesses`: Public business discovery listing.
  - `GET /businesses/:slug`: Detailed business profile by slug.
  - `PUT /businesses/:id`: Update Business (Validates `ownerId` authorization).
  - `DELETE /businesses/:id`: Delete Business (Validates `ownerId` authorization).
  - `GET /businesses/admin/all` & `PUT /businesses/admin/:id/status`: Admin listing & approval workflow (`ADMIN`).

- **Funding Opportunities (`FundingOpportunitiesController`)**:
  - `POST /businesses/:businessId/funding-opportunities`: Publish funding opportunity.
  - `GET /businesses/:businessId/funding-opportunities`: Retrieve funding opportunities list.
  - `PUT /businesses/:businessId/funding-opportunities/:id`: Update funding opportunity.
  - `DELETE /businesses/:businessId/funding-opportunities/:id`: Delete funding opportunity.

- **Amazon S3 Media Upload (`UploadController` & `UploadService`)**:
  - `POST /upload`: Uploads image files (up to 5MB, supports jpg, png, gif, webp) to Amazon S3 / MinIO.
  - Integrates `@aws-sdk/client-s3` (`PutObjectCommand`, `PutBucketPolicyCommand`).

- **Admin & Change Proposals (`AdminController` & `ProposalsController`)**:
  - `GET /admin/stats`: Overview system statistics.
  - `POST /admin/proposals/business/:id`: Create JSON change proposal.
  - `POST /proposals/:id/approve` & `POST /proposals/:id/reject`: Founder Diff/Merge review & approval.

#### 3. Cryptographic RSA JWT Signature Verification & Issuer `us-east-1` (`CognitoStrategy`)

Protected API requests are verified by `CognitoStrategy` using `jwks-rsa`:

```typescript
@Injectable()
export class CognitoStrategy extends PassportStrategy(Strategy, 'cognito') {
  constructor() {
    const userPoolId = process.env.COGNITO_USER_POOL_ID;
    const region = process.env.AWS_REGION || 'us-east-1';

    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      audience: process.env.COGNITO_CLIENT_ID,
      issuer: `https://cognito-idp.${region}.amazonaws.com/${userPoolId}`,
      algorithms: ['RS256'],
      secretOrKeyProvider: passportJwtSecret({
        cache: true,
        rateLimit: true,
        jwksRequestsPerMinute: 5,
        jwksUri: `https://cognito-idp.${region}.amazonaws.com/${userPoolId}/.well-known/jwks.json`,
      }),
    });
  }
}
```

#### 4. Dual-Layer Authorization Guard

The system combines `JwtAuthGuard` (verifies user identity) and `RolesGuard` (verifies `UserRole` & Cognito Group `ADMIN` permissions):

```typescript
@UseGuards(JwtAuthGuard, RolesGuard)
@Roles(Role.ADMIN)
@Get('admin/all')
findAllForAdmin() {
  return this.businessesService.findAllForAdmin(...);
}
```
