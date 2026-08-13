---
title: "Cấu hình Hạ tầng AWS"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Cấu hình Hạ tầng AWS — VPC, RDS, EC2, S3, CloudFront & API Gateway

Phần này hướng dẫn cách xây dựng toàn bộ hạ tầng AWS cho ứng dụng **Startups Blogs** bao gồm mạng riêng ảo, cơ sở dữ liệu, máy chủ backend, lưu trữ tĩnh và phân phối nội dung.

#### Tổng quan Kiến trúc

Hệ thống sử dụng các dịch vụ AWS sau:

| Dịch vụ | Vai trò |
|---------|---------|
| **Amazon VPC** | Mạng riêng ảo, cô lập tài nguyên |
| **Amazon RDS** | Cơ sở dữ liệu PostgreSQL được quản lý |
| **Amazon EC2** | Máy chủ chạy NestJS Backend |
| **Amazon S3** | Lưu trữ media (ảnh, tệp đính kèm) |
| **Amazon CloudFront** | CDN phân phối Frontend React & media |
| **Amazon API Gateway** | Cổng API kết nối Frontend với Backend |
| **Amazon Cognito** | Xác thực người dùng (xem mục 5.4) |

#### Nội dung

1. [VPC & Security Groups](5.3.1-VPC-Networking/)
2. [RDS PostgreSQL Database](5.3.2-RDS-Database/)
3. [EC2 & Backend Deployment](5.3.3-EC2-Backend/)
4. [S3 Bucket & CloudFront](5.3.4-S3-CloudFront/)
5. [API Gateway](5.3.5-API-Gateway/)
