---
title: "Resource Cleanup"
date: 2026-08-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### AWS Resource Cleanup & Workshop Conclusion

To avoid incurring unexpected cloud charges after completing the workshop, follow these steps to tear down testing resources using Terraform.

#### 1. Automated AWS Cloud Infrastructure Cleanup via Terraform
Run the Terraform destroy command to automatically remove 100% of provisioned AWS resources (VPC, EC2, RDS, Cognito, API Gateway, S3, CloudFront, CloudWatch) in region **`us-east-1`**:

```bash
cd terraform
terraform destroy -auto-approve
```

#### 2. Stop Local PostgreSQL Database & MinIO
Tear down local development containers:

```bash
docker-compose down -v
```

#### 3. Workshop Conclusion
In this workshop, you have successfully:
- Understood the full enterprise AWS cloud architecture of the **Startups Blogs** platform (Region: `us-east-1`).
- Automated 100% of AWS cloud infrastructure (VPC, EC2, RDS, Cognito, API Gateway, S3, CloudFront, CloudWatch) using **Terraform (IaC)**.
- Mastered configuring and integrating **Amazon Cognito User Pools** and Cognito Group `ADMIN` synchronization.
- Implemented complete **REST APIs** for business CRUD, funding opportunity publishing, S3 image uploads, and Admin Dashboard moderation.
- Verified token RSA cryptographic signatures using `jwks-rsa` against JWKS `us-east-1`.
- Established a clear boundary between verified implemented features and future enhancement roadmaps.
