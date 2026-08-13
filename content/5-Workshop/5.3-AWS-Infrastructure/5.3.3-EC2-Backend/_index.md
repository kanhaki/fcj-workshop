---
title: "EC2 & Backend Deployment"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 5.3.3 </b> "
---

### EC2 Instance Setup & NestJS Backend Deployment

#### Step 1 — Launch EC2 Instance

Go to **AWS Console** → **EC2** → **Launch instance**.

Basic configuration:
- **Name**: `startups-blogs-backend`
- **AMI**: **Ubuntu Server 26.04 LTS** (HVM), SSD Volume Type
- **Instance type**: `t3.micro`

![Step 1 - Select AMI and Instance Type](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step1-launch.png)
<p align="center"><i>Figure: Select Ubuntu 26.04 and t3.micro</i></p>

---

#### Step 2 — Configure Key Pair and Network

In the **Key pair** section:
- Click **Create new key pair** → name it `startups-blogs-key` → download the `.pem` file

In the **Network settings** section:
- **VPC**: Select the created VPC
- **Subnet**: Select a Public subnet
- **Auto-assign public IP**: Enable
- **Security group**: Select `EC2-Security-Group`

![Step 2 - Key Pair and Network](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step2-network.png)
<p align="center"><i>Figure: Key Pair and Network Settings Configuration</i></p>

---

#### Step 3 — Launch and SSH into EC2

Click **Launch instance**. Once the Instance state is **Running**, copy the **Public IPv4 address**.

SSH into EC2:
```bash
chmod 400 startups-blogs-key.pem
ssh -i startups-blogs-key.pem ubuntu@YOUR_EC2_PUBLIC_IP
```

![Step 3 - EC2 Running](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step3-running.png)
<p align="center"><i>Figure: EC2 Instance is in Running state</i></p>

---

#### Step 4 — Install Node.js and PM2

Run the following commands in the EC2 terminal:
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Node.js 20.x
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Install PM2
sudo npm install -g pm2

# Verify installation
node --version && npm --version && pm2 --version
```

![Step 4 - Install Node.js](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step4-nodejs.png)
<p align="center"><i>Figure: Node.js and PM2 installed successfully</i></p>

---

#### Step 5 — Clone Repository and Create .env file

```bash
# Clone source code
git clone https://github.com/YOUR_USERNAME/Startups_Blogs.git ~/Startup_Blogs
cd ~/Startup_Blogs/backend

# Install dependencies
npm install

# Create .env file
nano .env
```

`.env` file content:
```env
DATABASE_URL="postgresql://postgres:PASSWORD@YOUR-RDS-ENDPOINT:5432/postgres?schema=public"
COGNITO_USER_POOL_ID="us-east-1_XXXXXXXXX"
COGNITO_CLIENT_ID="YOUR_CLIENT_ID"
AWS_REGION="us-east-1"
AWS_S3_BUCKET="startups-blogs-media"
AWS_S3_ENDPOINT="https://s3.us-east-1.amazonaws.com"
AWS_S3_REGION="us-east-1"
AWS_S3_ACCESS_KEY="YOUR_ACCESS_KEY"
AWS_S3_SECRET_KEY="YOUR_SECRET_KEY"
```

![Step 5 - .env file](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step5-env.png)
<p align="center"><i>Figure: .env file content with all environment variables</i></p>

---

#### Step 6 — Build and Run Backend with PM2

```bash
# Generate Prisma client
npx prisma generate

# Build TypeScript to JavaScript
npm run build

# Run with PM2
pm2 start dist/src/main.js --name startups-backend
pm2 save && pm2 startup
```

Verify backend is running:
```bash
pm2 status
curl -I http://localhost:3000
```

![Step 6 - PM2 Status](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step6-pm2.png)
<p align="center"><i>Figure: PM2 shows startups-backend is online</i></p>
