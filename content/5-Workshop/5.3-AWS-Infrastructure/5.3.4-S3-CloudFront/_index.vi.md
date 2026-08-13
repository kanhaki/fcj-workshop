---
title: "S3 Bucket & CloudFront"
date: 2026-08-01
weight: 4
chapter: false
pre: " <b> 5.3.4 </b> "
---

### Thiết lập S3 Bucket & CloudFront Distribution

#### Bước 1 — Tạo S3 Bucket cho Media

Truy cập **AWS Console** → **S3** → **Create bucket**.

Điền thông tin:
- **Bucket name**: `startups-blogs-media`
- **Region**: `us-east-1`
- **Block Public Access**: Bỏ chọn *"Block all public access"* → tích xác nhận

Nhấn **Create bucket**.

![Bước 1 - Tạo Media Bucket](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step1-media-bucket.png)
<p align="center"><i>Hình: Tạo S3 Bucket cho Media với Public Access</i></p>

---

#### Bước 2 — Cấu hình CORS cho Media Bucket

Vào bucket `startups-blogs-media` → tab **Permissions** → cuộn xuống **Cross-origin resource sharing (CORS)** → nhấn **Edit**.

Dán nội dung sau:
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": []
  }
]
```

Nhấn **Save changes**.

![Bước 2 - CORS Configuration](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step2-cors.png)
<p align="center"><i>Hình: Cấu hình CORS cho phép Frontend upload ảnh</i></p>

---

#### Bước 3 — Tạo S3 Bucket cho Frontend

Tạo bucket thứ hai:
- **Bucket name**: `startups-blogs-frontend`
- **Region**: `us-east-1`
- **Block Public Access**: Giữ mặc định (CloudFront quản lý)

Sau khi tạo xong, vào **Properties** → cuộn xuống **Static website hosting** → **Edit**:
- **Enable** Static website hosting
- **Index document**: `index.html`
- **Error document**: `index.html`

![Bước 3 - Static Website Hosting](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step3-static-hosting.png)
<p align="center"><i>Hình: Bật Static Website Hosting cho Frontend Bucket</i></p>

---

#### Bước 4 — Upload Frontend lên S3

Build Frontend và upload:
```bash
cd frontend
npm run build
aws s3 sync dist/ s3://startups-blogs-frontend --delete
```

---

#### Bước 5 — Tạo CloudFront Distribution

Truy cập **CloudFront** → **Create distribution**.

Cấu hình:
- **Origin domain**: Chọn bucket `startups-blogs-frontend`
- **Origin access**: **Origin access control (OAC)** → Create new OAC
- **Default root object**: `index.html`

![Bước 5 - Tạo Distribution](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step5-distribution.png)
<p align="center"><i>Hình: Cấu hình Origin cho CloudFront Distribution</i></p>

---

#### Bước 6 — Cấu hình Error Pages và Deploy

Trong tab **Error pages** → **Create custom error response**:
Thêm lần lượt 2 Error Pages (cho lỗi 403 và 404):
- **HTTP error code**: 403 (và 404 cho cấu hình tiếp theo)
- **Response page path**: `/index.html`
- **HTTP response code**: 200

*(Bước này giúp React Router hoạt động đúng khi refresh trang hoặc khi đường dẫn không tồn tại)*

Nhấn **Create distribution** → chờ trạng thái **Enabled** (khoảng 5 phút).

Ghi lại **Distribution domain name**: `xxxxxxxx.cloudfront.net`

![Bước 6 - CloudFront Enabled](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step6-enabled.png)
<p align="center"><i>Hình: CloudFront Distribution đang hoạt động với domain name</i></p>
