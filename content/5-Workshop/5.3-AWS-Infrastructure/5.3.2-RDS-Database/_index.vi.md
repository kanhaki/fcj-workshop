---
title: "RDS PostgreSQL Database"
date: 2026-08-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

### Thiết lập Amazon RDS PostgreSQL

#### Bước 1 — Mở RDS Console và Tạo Database

Vào **AWS Console** → tìm **RDS** → chọn **Databases** → click **Create database**.

Chọn:
- **Standard create**
- **Engine type**: PostgreSQL
- **Engine Version**: PostgreSQL 16.x

![Bước 1 - Chọn RDS Engine](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step1-engine.png)
<p align="center"><i>Hình: Chọn PostgreSQL làm Database Engine</i></p>

---

#### Bước 2 — Cấu hình Instance

Trong phần **Settings**:
- **DB instance identifier**: `startups-blogs-db`
- **Master username**: `postgres`
- **Master password**: *(đặt mật khẩu mạnh, ghi lại để dùng sau)*

Trong phần **DB instance class**:
- Chọn **db.t3.micro** (Free Tier)
- **Storage**: 20 GB, loại gp2

![Bước 2 - Cấu hình Instance](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step2-instance.png)
<p align="center"><i>Hình: Cấu hình DB Instance class và Storage</i></p>

---

#### Bước 3 — Cấu hình Kết nối (Connectivity)

Trong phần **Connectivity**:
- **VPC**: Chọn VPC đã tạo ở bước 5.3.1
- **DB subnet group**: Tạo mới hoặc chọn subnet group trong VPC
- **Public access**: **No** *(RDS chỉ kết nối nội bộ qua VPC)*
- **VPC security group**: Chọn **RDS-Security-Group** đã tạo

![Bước 3 - Cấu hình Connectivity](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step3-connectivity.png)
<p align="center"><i>Hình: Cấu hình VPC và Security Group cho RDS</i></p>

---

#### Bước 4 — Tạo Database và chờ khởi tạo

Kéo xuống cuối trang → nhấn **Create database**.

Quá trình khởi tạo mất khoảng **5–10 phút**. Chờ đến khi trạng thái chuyển sang **Available**.

![Bước 4 - RDS Available](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step4-available.png)
<p align="center"><i>Hình: RDS Instance ở trạng thái Available</i></p>

---

#### Bước 5 — Lấy Endpoint và tạo DATABASE_URL

Nhấn vào tên DB Instance → vào tab **Connectivity & security** → sao chép **Endpoint**.

Tạo connection string để dùng trong file `.env` của Backend:

```bash
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@YOUR_ENDPOINT:5432/postgres?schema=public"
```

![Bước 5 - Lấy Endpoint](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.2-step5-endpoint.png)
<p align="center"><i>Hình: Endpoint của RDS dùng để kết nối từ Backend</i></p>
