---
title: "Prerequisites"
date: 2026-08-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### Environment Setup, Terraform & Database Preparation

Before proceeding with Amazon Cognito configuration and full-stack cloud deployment, ensure the following local development environment is prepared.

#### 1. Software Requirements
- **Node.js**: Version 18+ or 20+ LTS.
- **npm** / **yarn** / **pnpm**: Package manager.
- **Terraform**: Version v1.5+ for automated cloud infrastructure provisioning.
- **AWS CLI**: Installed and configured with region **`us-east-1`** (N. Virginia).
- **PostgreSQL Database**: Running locally via Docker (`docker-compose.yml` on port `5433`) or Amazon RDS.
- **Docker**: For PostgreSQL and MinIO S3 local container orchestration.

#### 2. Start Local Containers (PostgreSQL & MinIO)
Run the following command in the project root to start the local database and S3-compatible storage.
```bash
docker-compose up -d
```
![Docker Compose Output](/images/5-Workshop/5.2-Prerequiste/docker-compose.png)

#### 3. AWS CLI Authentication
Verify that your AWS CLI is properly authenticated in region `us-east-1` and has the necessary permissions to provision resources.
```bash
aws sts get-caller-identity
```

#### 4. Database Schema Initialization via Prisma ORM
The Startups Blogs domain data model is declared inside `backend/prisma/schema.prisma`. Execute the following commands to generate Prisma Client and apply migrations:

```bash
cd backend
npx prisma generate
npx prisma db push
```
![Prisma DB Push](/images/5-Workshop/5.2-Prerequiste/prisma-push.png)

#### 5. Seed Reference Data
Seed taxonomy records for industries, business types, stages, articles, and sample accounts into your database:

```bash
npx prisma db seed
```
![Prisma Seed](/images/5-Workshop/5.2-Prerequiste/prisma-seed.png)