---
title: "VPC & Security Groups"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

### Amazon VPC & Security Groups Setup

#### Step 1 — Create VPC

Go to **AWS Console** → search for **VPC** → select **Your VPCs** → click **Create VPC**.

Fill in the information:
- **Name tag**: `Startups-Blogs-vpc`
- **IPv4 CIDR block**: `10.0.0.0/16`
- **Tenancy**: Default

Click **Create VPC**.

![Step 1 - Create VPC](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step1-create-vpc.png)
<p align="center"><i>Figure: Create VPC with CIDR 10.0.0.0/16</i></p>

---

#### Step 2 — Create Subnets

On the left navigation pane, select **Subnets** → **Create subnet** → select the newly created VPC.

Create the subnets (if using Terraform, these will be created automatically based on the `terraform/` configuration):

| Name | CIDR | Type | AZ |
|-----|------|------|----|
| `Startups-Blogs-subnet-public1-us-east-1a` | `10.0.0.0/20` | Public | us-east-1a |
| `Startups-Blogs-subnet-private1-us-east-1a` | `10.0.128.0/20` | Private | us-east-1a |
| `Startups-Blogs-subnet-private2` | `10.0.200.0/24` | Private | us-east-1b |

![Step 2 - Create Subnets](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step2-subnets.png)
<p align="center"><i>Figure: List of created Subnets inside the VPC</i></p>

---

#### Step 3 — Create Internet Gateway

Select **Internet Gateways** → **Create internet gateway**.
- **Name tag**: `Startups-Blogs-igw`

After creating, click **Actions** → **Attach to VPC** → select the VPC.

![Step 3 - Internet Gateway](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step3-igw.png)
<p align="center"><i>Figure: Internet Gateway attached to the VPC</i></p>

---

#### Step 4 — Create Security Group for EC2

Select **Security Groups** → **Create security group**.
- **Security group name**: `EC2-Security-Group`
- **VPC**: Select the VPC

Add **Inbound rules**:

| Port | Protocol | Source | Purpose |
|------|----------|--------|---------|
| 22 | TCP | 0.0.0.0/0 | SSH |
| 3000 | TCP | 0.0.0.0/0 | NestJS Backend API |

Click **Create security group**.

![Step 4 - EC2 Security Group](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step4-ec2-sg.png)
<p align="center"><i>Figure: EC2 Security Group with Port 22 and 3000</i></p>

---

#### Step 5 — Create Security Group for RDS

Create another Security Group:
- **Security group name**: `RDS-Security-Group`
- **VPC**: Select the VPC

Add **Inbound rule**:

| Port | Protocol | Source | Purpose |
|------|----------|--------|---------|
| 5432 | TCP | EC2-Security-Group | PostgreSQL from EC2 |

> Set the Source to **EC2-Security-Group** (not a static IP) to ensure only the EC2 instance can connect to RDS.

![Step 5 - RDS Security Group](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step5-rds-sg.png)
<p align="center"><i>Figure: RDS Security Group allows connections only from EC2</i></p>
