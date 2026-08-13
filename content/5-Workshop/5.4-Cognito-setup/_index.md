---
title: "Cognito Configuration"
date: 2026-08-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Amazon Cognito User Pool, App Client & Cognito Groups Setup (`us-east-1`)

In this section, we manage **Amazon Cognito User Pool** identities securely for the Startups Blogs platform in the **`us-east-1`** region.

#### 1. Preliminary Cognito Configuration Overview
For the Startups Blogs system, the core security policies of the Cognito User Pool are configured with the following enterprise standards:
- **Sign-in experience**: Users authenticate directly using their `Email`.
- **Password policy**: Enforces strong passwords (minimum 8 characters, requiring uppercase, lowercase, numbers, and special characters).
- **Email verification**: The system automatically dispatches a Verification Code via email upon new account registration.
- **App Client Security**: Integrates **SecretHash HMAC-SHA256** authentication flow. The NestJS Backend computes a cryptographic hash using the `ClientId` and `ClientSecret` before making any Cognito API calls, ensuring maximum security for the Microservices architecture.

#### 2. User Management
View and manage registered users in the Cognito User Pool.
1. Navigate to your User Pool in **Amazon Cognito** (`us-east-1`).
2. In the left menu, select **User management > Users**.
3. Here you can verify all registered accounts, their email verification status, and whether they are confirmed.

![Cognito Users](/images/5-Workshop/5.4-Cognito-setup/users.png)

#### 3. Cognito User Pool Groups (ADMIN Role)
Create a User Pool Group named **`ADMIN`**. In the left menu, select **User management > Groups** to view the `ADMIN` group and its currently assigned members.

The system `ADMIN` role is synchronized with Cognito Group `ADMIN` using `CognitoGroupsService`:
- `AdminAddUserToGroupCommand`
- `AdminRemoveUserFromGroupCommand`

```typescript
// Inside cognito-groups.service.ts
const command = isAdmin
  ? new AdminAddUserToGroupCommand({ GroupName: 'ADMIN', Username: username, UserPoolId: userPoolId })
  : new AdminRemoveUserFromGroupCommand({ GroupName: 'ADMIN', Username: username, UserPoolId: userPoolId });
await this.client.send(command);
```

![Cognito ADMIN Group](/images/5-Workshop/5.4-Cognito-setup/group-admin.png)

#### 4. App Client Settings & Authentication Flows
1. In the left menu, select **Applications > App clients**.
2. Click on your App Client name (e.g., `startups-blogs-app`).
3. Under **App client information**, verify the **Client ID**.
4. Under **Authentication flows**, ensure flows like **Username and password** and **Secure remote password (SRP)** are enabled.

![Cognito App Client Settings](/images/5-Workshop/5.4-Cognito-setup/app-client.png)

#### 5. Environment Parameters
Record parameters for backend environment configuration (ensure `.env` files are ignored by git):

```env
AWS_REGION=us-east-1
COGNITO_USER_POOL_ID=us-east-1_xxxxxxxxx
COGNITO_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxx
COGNITO_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

![Cognito User Pool Overview](/images/5-Workshop/5.4-Cognito-setup/overview.png)
