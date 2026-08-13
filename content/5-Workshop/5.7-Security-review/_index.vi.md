---
title: "Tự động hóa Terraform & Bảo mật"
date: 2026-08-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

### Tự động hóa Hạ tầng bằng Terraform (IaC), Giám sát CloudWatch & Rà soát Bảo mật

Trong phần này, chúng em sẽ tìm hiểu cách toàn bộ hạ tầng Đám mây AWS của Startups Blogs được tự động hóa bằng **Terraform (Infrastructure as Code)** và thiết lập giám sát bằng **Amazon CloudWatch** tại Region **`us-east-1`**.

#### 1. Tự động hóa Hạ tầng bằng Terraform (`terraform/`)

Toàn bộ 100% tài nguyên Đám mây được khai báo trong thư mục `terraform/`:
- **Mạng VPC (`vpc.tf`)**: Tạo Virtual Private Cloud với 2 Public Subnets và 2 Private Subnets phân bổ trên các Availability Zones `us-east-1a` và `us-east-1b`.
- **Cơ sở dữ liệu RDS (`rds.tf`)**: Khởi tạo Amazon RDS cho PostgreSQL trong Private Subnet. Security Group của RDS chỉ cho phép duy nhất máy chủ EC2 kết nối qua cổng 5432.
- **Máy chủ Backend EC2 (`ec2.tf`)**: Khởi tạo máy chủ EC2 Ubuntu, chạy NestJS backend qua PM2 24/7.
- **Xác thực Cognito (`cognito.tf`)**: Tạo Cognito User Pool và Confidential App Client với Secret Key.
- **API Gateway (`apigateway.tf`)**: Định tuyến request từ HTTPS công cộng vào EC2 backend.
- **S3 & CloudFront (`s3_cloudfront.tf`)**: Lưu trữ tĩnh Frontend và cấu hình CloudFront CDN toàn cầu.
- **CloudWatch & Cảnh báo (`monitoring.tf`)**: Cấu hình Log Groups, CloudWatch Metric Alarms và gửi thông báo cảnh báo qua SNS Email.

Lệnh triển khai tự động hạ tầng trên CloudShell hoặc máy tính đã cài đặt Terraform:

```bash
cd terraform
terraform init
terraform apply -auto-approve
```

---

#### 2. Giám sát Hệ thống với Amazon CloudWatch (`monitoring.tf`)

CloudWatch đóng vai trò là hệ thống camera an ninh theo dõi toàn bộ sức khỏe hệ thống:
- **Log Groups**: Thu thập log thời gian thực từ API Gateway và EC2 Backend NestJS.
- **CloudWatch Dashboard**: Theo dõi chỉ số CPU Utilization, Memory, và Network I/O của EC2 và RDS.
- **SNS Alerts**: Tự động phát cảnh báo qua email (`alert_email`) khi CPU EC2 vượt ngưỡng 80% hoặc RDS gặp sự cố.

---

#### 3. Rà soát Bảo mật Tổng thể (Security Best Practices Review)

- **Bảo mật Hạ tầng Mạng**: RDS PostgreSQL giấu hoàn toàn trong Private Subnet, ngăn chặn ping hoặc truy cập trực tiếp từ Internet.
- **Bảo vệ Secret Key Server-side**: `COGNITO_CLIENT_SECRET` giữ an toàn trên NestJS backend, sử dụng HMAC-SHA256 `SECRET_HASH` cho mọi lệnh SDK.
- **Xác minh Chữ ký RSA JWT (`us-east-1`)**: Sử dụng `jwks-rsa` / `aws-jwt-verify` thẩm định trực tiếp chữ ký RSA của token từ JWKS.
- **Phân quyền Hai tầng (Dual Guard)**: Kiểm tra cả JWT Token và thuộc tính `ownerId` cho mọi thao tác chỉnh sửa dữ liệu doanh nghiệp.
- **Không lộ Bí mật Hệ thống**: Tuyệt đối không lưu vết chìa khóa bí mật, AWS Credentials hay Token thực tế trên tài liệu hoặc mã nguồn công khai.
