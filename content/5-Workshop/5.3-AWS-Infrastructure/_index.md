---
title: "AWS Infrastructure Setup"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### AWS Infrastructure Setup — VPC, RDS, EC2, S3, CloudFront & API Gateway

This section guides you through building the complete AWS infrastructure for the **Startups Blogs** application, including the virtual private network, managed database, backend server, static storage, and content delivery.

#### Architecture Overview

The system leverages the following AWS services:

| Service | Role |
|---------|------|
| **Amazon VPC** | Virtual private network, resource isolation |
| **Amazon RDS** | Managed PostgreSQL database |
| **Amazon EC2** | Server running the NestJS Backend |
| **Amazon S3** | Media storage (images, attachments) |
| **Amazon CloudFront** | CDN for React Frontend & media delivery |
| **Amazon API Gateway** | API gateway connecting Frontend to Backend |
| **Amazon Cognito** | User authentication (see section 5.4) |

#### Content

1. [VPC & Security Groups](5.3.1-VPC-Networking/)
2. [RDS PostgreSQL Database](5.3.2-RDS-Database/)
3. [EC2 & Backend Deployment](5.3.3-EC2-Backend/)
4. [S3 Bucket & CloudFront](5.3.4-S3-CloudFront/)
5. [API Gateway](5.3.5-API-Gateway/)
