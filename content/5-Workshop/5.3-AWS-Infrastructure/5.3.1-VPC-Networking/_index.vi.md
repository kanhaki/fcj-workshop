---
title: "VPC & Security Groups"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

### Thiết lập Amazon VPC & Security Groups

#### Bước 1 — Tạo VPC

Truy cập **AWS Console** → tìm kiếm **VPC** → chọn **Your VPCs** → nhấn **Create VPC**.

Điền thông tin:
- **Name tag**: `Startups-Blogs-vpc`
- **IPv4 CIDR block**: `10.0.0.0/16`
- **Tenancy**: Default

Nhấn **Create VPC**.

![Bước 1 - Tạo VPC](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step1-create-vpc.png)
<p align="center"><i>Hình: Tạo VPC với CIDR 10.0.0.0/16</i></p>

---

#### Bước 2 — Tạo Subnets

Trong thanh bên trái chọn **Subnets** → **Create subnet** → chọn VPC vừa tạo.

Tạo lần lượt các subnet (nếu dùng Terraform, các subnet sẽ được tạo tự động theo cấu hình trong `terraform/`):

| Tên | CIDR | Loại | AZ |
|-----|------|------|----|
| `Startups-Blogs-subnet-public1-us-east-1a` | `10.0.0.0/20` | Public | us-east-1a |
| `Startups-Blogs-subnet-private1-us-east-1a` | `10.0.128.0/20` | Private | us-east-1a |
| `Startups-Blogs-subnet-private2` | `10.0.200.0/24` | Private | us-east-1b |

![Bước 2 - Tạo Subnets](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step2-subnets.png)
<p align="center"><i>Hình: Danh sách các Subnet đã tạo trong VPC</i></p>

---

#### Bước 3 — Tạo Internet Gateway

Chọn **Internet Gateways** → **Create internet gateway**.
- **Name tag**: `Startups-Blogs-igw`

Sau khi tạo xong, nhấn **Actions** → **Attach to VPC** → chọn VPC vừa tạo.

![Bước 3 - Internet Gateway](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step3-igw.png)
<p align="center"><i>Hình: Internet Gateway đã được gắn vào VPC</i></p>

---

#### Bước 4 — Tạo Security Group cho EC2

Chọn **Security Groups** → **Create security group**.
- **Security group name**: `EC2-Security-Group`
- **VPC**: Chọn VPC vừa tạo

Thêm **Inbound rules**:

| Port | Protocol | Source | Mục đích |
|------|----------|--------|---------|
| 22 | TCP | 0.0.0.0/0 | SSH |
| 3000 | TCP | 0.0.0.0/0 | NestJS Backend API |

Nhấn **Create security group**.

![Bước 4 - EC2 Security Group](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step4-ec2-sg.png)
<p align="center"><i>Hình: Security Group cho EC2 với Port 22 và 3000</i></p>

---

#### Bước 5 — Tạo Security Group cho RDS

Tạo thêm một Security Group mới:
- **Security group name**: `RDS-Security-Group`
- **VPC**: Chọn VPC vừa tạo

Thêm **Inbound rule**:

| Port | Protocol | Source | Mục đích |
|------|----------|--------|---------|
| 5432 | TCP | EC2-Security-Group | PostgreSQL từ EC2 |

> Chọn Source là **EC2-Security-Group** (không phải IP tĩnh) để đảm bảo chỉ EC2 mới kết nối được vào RDS.

![Bước 5 - RDS Security Group](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.1-step5-rds-sg.png)
<p align="center"><i>Hình: Security Group cho RDS chỉ cho phép kết nối từ EC2</i></p>
