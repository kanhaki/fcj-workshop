---
title: "RDS PostgreSQL Database"
date: 2026-08-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

### Amazon RDS PostgreSQL Setup

#### Step 1 — Open RDS Console and Create Database

Go to **AWS Console** → search for **RDS** → select **Databases** → click **Create database**.

Select:
- **Standard create**
- **Engine type**: PostgreSQL
- **Engine Version**: PostgreSQL 16.x

![Step 1 - Select RDS Engine](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step1-engine.png)
<p align="center"><i>Figure: Select PostgreSQL as the Database Engine</i></p>

---

#### Step 2 — Configure Instance

In the **Settings** section:
- **DB instance identifier**: `startups-blogs-db`
- **Master username**: `postgres`
- **Master password**: *(set a strong password, save it for later)*

In the **DB instance class** section:
- Select **db.t3.micro** (Free Tier)
- **Storage**: 20 GB, gp2 type

![Step 2 - Configure Instance](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step2-instance.png)
<p align="center"><i>Figure: Configure DB Instance class and Storage</i></p>

---

#### Step 3 — Connectivity Configuration

In the **Connectivity** section:
- **VPC**: Select the VPC created in step 5.3.1
- **DB subnet group**: Create a new one or select an existing subnet group
- **Public access**: **No** *(RDS only connects internally via VPC)*
- **VPC security group**: Select the created **RDS-Security-Group**

![Step 3 - Connectivity Configuration](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step3-connectivity.png)
<p align="center"><i>Figure: Configure VPC and Security Group for RDS</i></p>

---

#### Step 4 — Create Database and Wait

Scroll to the bottom → click **Create database**.

The initialization process takes about **5–10 minutes**. Wait until the status changes to **Available**.

![Step 4 - RDS Available](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step4-available.png)
<p align="center"><i>Figure: RDS Instance is in the Available state</i></p>

---

#### Step 5 — Get Endpoint and Create DATABASE_URL

Click on the DB Instance name → go to the **Connectivity & security** tab → copy the **Endpoint**.

Create the connection string to use in the Backend's `.env` file:

```bash
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@YOUR_ENDPOINT:5432/postgres?schema=public"
```

![Step 5 - Get Endpoint](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step5-endpoint.png)
<p align="center"><i>Figure: RDS Endpoint used for Backend connections</i></p>
