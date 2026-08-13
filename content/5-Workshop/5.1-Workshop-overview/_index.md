---
title: "Workshop Overview"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Workshop Overview & Enterprise AWS Architecture

In this section, we cover the overall architecture of **Startups Blogs** and the cloud authentication flow powered by **Amazon Cognito (`us-east-1`)**.

#### 1. Enterprise AWS Architecture Diagram
The system is built according to Enterprise Microservices & Serverless best practices, isolating Frontend, Backend, Database, and Identity Management. 100% of the infrastructure is automated via **Terraform** (Infrastructure as Code).

![Startups Blogs System Architecture](/images/5-Workshop/5.1-Workshop-overview/AWS%20Architect.drawio.png)

#### 2. User Roles & Registration Boundary
The system defines 4 major roles (`UserRole`):
- **`BUSINESS_OWNER`**: Public self-registration. Manages business profiles and funding listings.
- **`INVESTOR`**: Public self-registration. Explores, searches, and evaluates investment opportunities.
- **`ENTERPRISE_PARTNER`**: Public self-registration. Participates in strategic partnerships and joint ventures.
- **`ADMIN`**: **NOT publicly registrable**. Synchronized with Cognito User Pool Group `ADMIN` via `CognitoGroupsService`. Administrators utilize the Admin Dashboard to approve business listings (`PUT /businesses/admin/:id/status`), moderate articles, and process Change Proposals.

#### 3. Implemented vs Planned Feature Matrix
- **IMPLEMENTED AND VERIFIED**:
  - Complete Terraform IaC codebase inside `terraform/` (Region: `us-east-1`).
  - Amazon RDS PostgreSQL & Prisma ORM Schema.
  - Business Write & Read APIs (`POST/GET/PUT/DELETE /businesses`).
  - Funding Opportunity APIs (`POST/GET/PUT/DELETE /businesses/:businessId/funding-opportunities`).
  - S3 Media Uploads (`POST /upload`).
  - Amazon Cognito Auth, SecretHash HMAC-SHA256, and Cognito Group `ADMIN` synchronization.
  - HttpOnly Signed Cookie security & RSA Token signature verification via `aws-jwt-verify` against JWKS `us-east-1`.
  - React 19 Frontend, Zustand state, Admin Dashboard (`/admin/*`), and Change Proposals.
  - Contact Requests (`POST /businesses/:businessId/contact-requests`).
- **PLANNED**:
  - Real-time Notification System (Notification Schema & WebSocket/polling).
  - Advanced multi-tier funding approval workflow.
  - Expanded automated E2E test coverage.

#### 4. Startups Blogs Web Interface

Below are some actual screenshots of the Startups Blogs web application after successful deployment:

**Home Page (Header):** An intuitive header interface displaying core features and main navigation.
![Home Page Header](/images/5-Workshop/5.1-Workshop-overview/home-page%20(1).png)

**Home Page (Content):** A list of highlighted startups, investment opportunities, and latest articles fetched from the Backend API.
![Home Page Content](/images/5-Workshop/5.1-Workshop-overview/home-page%20(2).png)

**Entity Relationship Diagram (ERD):** The database schema diagram detailing the PostgreSQL tables (`users`, `businesses`, `articles`) and their relationships (owns, writes, etc.).
![Entity Relationship Diagram (ERD)](/images/5-Workshop/5.1-Workshop-overview/Business%20Funding-2026-08-13-081827.png)