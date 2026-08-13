---
title: "API Gateway"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5.3.5 </b> "
---

### Thiết lập Amazon API Gateway

#### Bước 1 — Tạo HTTP API

Truy cập **AWS Console** → **API Gateway** → nhấn **Create API**.

Chọn **HTTP API** → nhấn **Build**.

Điền:
- **API name**: `startups-blogs-api`

Nhấn **Next** → **Next** → **Create**.

![Bước 1 - Tạo HTTP API](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step1-create-api.png)
<p align="center"><i>Hình: Tạo HTTP API với tên startups-blogs-api</i></p>

---

#### Bước 2 — Tạo Integration với EC2 Backend

Trong menu bên trái chọn **Integrations** → **Manage integrations** → **Create**.

Cấu hình:
- **Integration type**: HTTP URI
- **HTTP method**: ANY
- **URL endpoint**: `http://EC2_PUBLIC_IP:3000/{proxy}`

Nhấn **Create**.

![Bước 2 - Tạo Integration](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step2-integration.png)
<p align="center"><i>Hình: Integration trỏ đến EC2 Backend tại port 3000</i></p>

---

#### Bước 3 — Tạo Route proxy

Trong menu bên trái chọn **Routes** → **Create**.

Cấu hình:
- **Method**: `ANY`
- **Path**: `/{proxy+}`
- **Integration target**: Chọn integration vừa tạo ở Bước 2

Nhấn **Create**.

![Bước 3 - Tạo Route](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step3-route.png)
<p align="center"><i>Hình: Route ANY /{proxy+} chuyển tiếp mọi request đến Backend</i></p>

---

#### Bước 4 — Cấu hình CORS

Trong menu bên trái chọn **CORS** → **Configure**.

Điền:
- **Access-Control-Allow-Origin**: `*`
- **Access-Control-Allow-Methods**: `GET, POST, PUT, DELETE, OPTIONS, PATCH`
- **Access-Control-Allow-Headers**: `*`

Nhấn **Save**.

![Bước 4 - Cấu hình CORS](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step4-cors.png)
<p align="center"><i>Hình: Cấu hình CORS cho phép Frontend gọi API</i></p>

---

#### Bước 5 — Lấy Invoke URL và cập nhật Frontend

Vào **Stages** → chọn stage `$default` → sao chép **Invoke URL**.

```
https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com
```

Cập nhật biến môi trường trong Frontend:
```env
# frontend/.env.production
VITE_API_URL=https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com
```

Build lại Frontend và upload lên S3:
```bash
npm run build
aws s3 sync dist/ s3://startups-blogs-frontend --delete
```

![Bước 5 - Invoke URL](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step5-invoke-url.png)
<p align="center"><i>Hình: Invoke URL của API Gateway dùng cho Frontend</i></p>
