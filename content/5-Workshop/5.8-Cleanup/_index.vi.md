---
title: "Dọn dẹp tài nguyên"
date: 2026-08-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Dọn dẹp Tài nguyên AWS & Tổng kết Workshop

Để tránh phát sinh chi phí không mong muốn sau khi hoàn thành bài thực hành, hãy tiến hành dọn dẹp các tài nguyên thử nghiệm bằng Terraform.

#### 1. Dọn dẹp Tài nguyên Đám mây AWS bằng Terraform
Sử dụng lệnh Terraform để tiêu hủy tự động toàn bộ 100% tài nguyên đã khởi tạo (VPC, EC2, RDS, Cognito, API Gateway, S3, CloudFront, CloudWatch) tại Region **`us-east-1`**:

```bash
cd terraform
terraform destroy -auto-approve
```

#### 2. Dọn dẹp Cơ sở dữ liệu Local PostgreSQL & MinIO
Dừng các Docker container thử nghiệm trên máy local:

```bash
docker-compose down -v
```

#### 3. Kết luận bài Workshop
Thông qua bài thực hành này, bạn đã:
- Hiểu rõ kiến trúc hạ tầng Đám mây Enterprise của hệ thống **Startups Blogs** (Region: `us-east-1`).
- Tự động hóa 100% tài nguyên đám mây (VPC, EC2, RDS, Cognito, API Gateway, S3, CloudFront, CloudWatch) bằng **Terraform (IaC)**.
- Nắm vững quy trình cấu hình và tích hợp **Amazon Cognito User Pool** cùng nhóm Cognito Group `ADMIN`.
- Triển khai thành công hệ thống **REST APIs** đầy đủ các tính năng Đọc/Ghi doanh nghiệp, đăng tin gọi vốn, tải ảnh S3 và Admin Dashboard.
- Thẩm định tính an toàn của token xác thực qua chữ ký RSA với `jwks-rsa` từ JWKS `us-east-1`.
- Phân định rõ ràng giữa các tính năng đã triển khai thực tế và lộ trình mở rộng trong tương lai.
