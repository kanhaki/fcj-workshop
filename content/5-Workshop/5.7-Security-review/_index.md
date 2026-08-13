---
title: "Terraform Automation & Security"
date: 2026-08-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

### Infrastructure as Code (Terraform), CloudWatch Monitoring & Security Review

In this section, we explore how the entire AWS Cloud infrastructure for Startups Blogs is automated using **Terraform (IaC)** and how monitoring is established via **Amazon CloudWatch** in the **`us-east-1`** region.

#### 1. Infrastructure Automation with Terraform (`terraform/`)

100% of AWS cloud resources are declared in the `terraform/` directory:
- **VPC Infrastructure (`vpc.tf`)**: Creates a Virtual Private Cloud with 2 Public Subnets and 2 Private Subnets spanning Availability Zones `us-east-1a` and `us-east-1b`.
- **RDS Database (`rds.tf`)**: Provisions Amazon RDS PostgreSQL in Private Subnets. Security Groups restrict database port 5432 access strictly to the EC2 instance.
- **EC2 Compute (`ec2.tf`)**: Provisions an Ubuntu EC2 instance running NestJS backend via PM2 24/7.
- **Cognito Auth (`cognito.tf`)**: Declares User Pool and Confidential App Client with Secret Key.
- **API Gateway (`apigateway.tf`)**: Routes public HTTPS API requests to the backend EC2 server.
- **S3 & CloudFront (`s3_cloudfront.tf`)**: Configures S3 static frontend hosting and CloudFront global CDN distribution.
- **CloudWatch & Alerts (`monitoring.tf`)**: Configures Log Groups, CloudWatch Alarms, and SNS Email notifications.

Automated deployment commands (execute on CloudShell or a machine with Terraform installed):

```bash
cd terraform
terraform init
terraform apply -auto-approve
```

---

#### 2. System Monitoring with Amazon CloudWatch (`monitoring.tf`)

CloudWatch acts as the central observability platform:
- **Log Groups**: Centralized real-time logging for API Gateway and EC2 NestJS Backend.
- **CloudWatch Dashboard**: Tracks CPU Utilization, Memory, and Network I/O metrics across EC2 and RDS.
- **SNS Alerts**: Automatically dispatches SNS Email notifications (`alert_email`) when EC2 CPU exceeds 80% or RDS health degrades.

---

#### 3. Security Best Practices Review

- **Network Infrastructure Security**: RDS PostgreSQL is heavily isolated in a Private Subnet, blocking direct internet access and ICMP ping.
- **Server-side Secret Protection**: `COGNITO_CLIENT_SECRET` is secured on the backend, generating an HMAC-SHA256 `SECRET_HASH` for all Cognito SDK interactions.
- **Cryptographic RSA JWT Verification (`us-east-1`)**: The backend utilizes `jwks-rsa` to mathematically verify the Token's RSA signature against Cognito's JWKS endpoint.
- **Dual Guard Authorization**: Validates both the cryptographic JWT and the relational `ownerId` for all business data mutations.
- **Zero Secrets Exposure**: Strict prevention of hardcoding AWS Credentials, Secret Keys, or real Tokens in public repositories or documentation.
