---
title: "Chuẩn bị môi trường"
date: 2026-08-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### Chuẩn bị Môi trường, Terraform & Cơ sở dữ liệu

Trước khi thực hiện các bước cấu hình Amazon Cognito và hạ tầng Đám mây AWS, bạn cần chuẩn bị các công cụ môi trường sau.

#### 1. Yêu cầu công cụ (Prerequisites)
- **Node.js**: Phiên bản 18+ hoặc 20+ LTS.
- **npm** / **yarn** / **pnpm**: Trình quản lý gói phụ thuộc.
- **Terraform**: Phiên bản v1.5+ để khởi tạo hạ tầng Đám mây tự động.
- **AWS CLI**: Đã cài đặt và cấu hình credentials với khu vực **`us-east-1`** (N. Virginia).
- **PostgreSQL Database**: Đã khởi chạy locally qua Docker (`docker-compose.yml` tại cổng `5433`) hoặc dịch vụ Amazon RDS PostgreSQL.
- **Docker**: Khởi chạy container PostgreSQL và MinIO S3 simulation.

#### 2. Khởi chạy Container Local (PostgreSQL & MinIO)
Chạy lệnh sau tại thư mục gốc của dự án để khởi động cơ sở dữ liệu và kho lưu trữ S3 giả lập ở dưới máy local.
```bash
docker-compose up -d
```
![Khởi chạy Docker Compose](/images/5-Workshop/5.2-Prerequiste/docker-compose.png)
<p align="center"><i>Hình: Khởi chạy Docker Compose</i></p>

#### 3. Xác thực AWS CLI
Kiểm tra xem AWS CLI của bạn đã được xác thực thành công và trỏ đúng vào region `us-east-1` chưa.
```bash
aws sts get-caller-identity
```

#### 4. Cấu hình cơ sở dữ liệu với Prisma ORM
Mô hình dữ liệu của Startups Blogs được định nghĩa chi tiết trong `backend/prisma/schema.prisma`. Khởi tạo và đồng bộ cơ sở dữ liệu bằng lệnh:

```bash
cd backend
npx prisma generate
npx prisma db push
```
![Khởi tạo Database Prisma](/images/5-Workshop/5.2-Prerequiste/prisma-push.png)
<p align="center"><i>Hình: Khởi tạo Database Prisma</i></p>

#### 5. Khởi tạo dữ liệu mẫu (Seed Data)

Đăng ký dữ liệu mẫu cho danh mục ngành nghề (Industries), loại hình doanh nghiệp, giai đoạn phát triển, bài viết mẫu và tài khoản thử nghiệm:

```bash
npx prisma db seed
```
![Dữ liệu mẫu Prisma](/images/5-Workshop/5.2-Prerequiste/prisma-seed.png)
<p align="center"><i>Hình: Dữ liệu mẫu Prisma</i></p>

