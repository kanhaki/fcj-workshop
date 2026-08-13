---
title: "EC2 & Backend Deployment"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 5.3.3 </b> "
---

### Thiết lập EC2 Instance & Deploy NestJS Backend

#### Bước 1 — Launch EC2 Instance

Vào **AWS Console** → **EC2** → **Launch instance**.

Cấu hình cơ bản:
- **Name**: `startups-blogs-backend`
- **AMI**: **Ubuntu Server 26.04 LTS** (HVM), SSD Volume Type
- **Instance type**: `t3.micro`

![Bước 1 - Chọn AMI và Instance Type](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step1-launch.png)
<p align="center"><i>Hình: Chọn Ubuntu 26.04 và t3.micro</i></p>

---

#### Bước 2 — Cấu hình Key Pair và Network

Trong phần **Key pair**:
- Nhấn **Create new key pair** → đặt tên `startups-blogs-key` → tải file `.pem` về máy

Trong phần **Network settings**:
- **VPC**: Chọn VPC đã tạo
- **Subnet**: Chọn Public subnet
- **Auto-assign public IP**: Enable
- **Security group**: Chọn `EC2-Security-Group`

![Bước 2 - Key Pair và Network](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step2-network.png)
<p align="center"><i>Hình: Cấu hình Key Pair và Network Settings</i></p>

---

#### Bước 3 — Launch và SSH vào EC2

Nhấn **Launch instance**. Sau khi Instance chuyển sang trạng thái **Running**, sao chép **Public IPv4 address**.

SSH vào EC2:
```bash
chmod 400 startups-blogs-key.pem
ssh -i startups-blogs-key.pem ubuntu@YOUR_EC2_PUBLIC_IP
```

![Bước 3 - EC2 Running](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step3-running.png)
<p align="center"><i>Hình: EC2 Instance đang ở trạng thái Running</i></p>

---

#### Bước 4 — Cài đặt Node.js và PM2

Chạy các lệnh sau trong terminal EC2:
```bash
# Cập nhật hệ thống
sudo apt update && sudo apt upgrade -y

# Cài Node.js 20.x
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Cài PM2
sudo npm install -g pm2

# Kiểm tra
node --version && npm --version && pm2 --version
```

![Bước 4 - Cài Node.js](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step4-nodejs.png)
<p align="center"><i>Hình: Node.js và PM2 đã được cài đặt thành công</i></p>

---

#### Bước 5 — Clone Repository và tạo file .env

```bash
# Clone source code
git clone https://github.com/YOUR_USERNAME/Startups_Blogs.git ~/Startup_Blogs
cd ~/Startup_Blogs/backend

# Cài dependencies
npm install

# Tạo file .env
nano .env
```

Nội dung file `.env`:
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

![Bước 5 - File .env](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step5-env.png)
<p align="center"><i>Hình: Nội dung file .env với đầy đủ biến môi trường</i></p>

---

#### Bước 6 — Build và khởi chạy Backend với PM2

```bash
# Generate Prisma client
npx prisma generate

# Build TypeScript sang JavaScript
npm run build

# Khởi chạy bằng PM2
pm2 start dist/src/main.js --name startups-backend
pm2 save && pm2 startup
```

Kiểm tra backend đang chạy:
```bash
pm2 status
curl -I http://localhost:3000
```

![Bước 6 - PM2 Status](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.3-step6-pm2.png)
<p align="center"><i>Hình: PM2 hiển thị startups-backend đang online</i></p>
