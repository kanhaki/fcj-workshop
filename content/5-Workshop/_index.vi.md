---
title: "Workshop"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Tích hợp Hạ tầng Đám mây AWS & Xác thực Amazon Cognito cho Ứng dụng Startups Blogs (React + NestJS + PostgreSQL + Terraform)

#### Tổng quan

Trong bài thực hành (Workshop) này, bạn sẽ học cách thiết kế, xây dựng và tự động hóa toàn bộ hạ tầng đám mây Enterprise trên **AWS (Region: `us-east-1`)** cho nền tảng kết nối đầu tư **Startups Blogs**.

Hệ thống kết hợp kiến trúc Full-Stack bao gồm **React 19 (TypeScript, Vite)** ở Frontend, **NestJS REST API** ở Backend, cơ sở dữ liệu **Amazon RDS PostgreSQL**, lưu trữ ảnh **Amazon S3**, CDN **CloudFront**, cửa ngõ API **API Gateway**, hệ thống xác thực **Amazon Cognito**, giám sát **CloudWatch** và 100% mã nguồn hạ tầng **Terraform (Infrastructure as Code)**.

#### Điểm nổi bật của giải pháp
+ **Hạ tầng Tự động hóa với Terraform**: Toàn bộ tài nguyên AWS (VPC, EC2, RDS, Cognito, API Gateway, S3, CloudFront, CloudWatch) được khai báo bằng mã nguồn Terraform trong thư mục `terraform/`.
+ **Ủy quyền Quản lý Identity**: Không lưu trữ mật khẩu trực tiếp trong cơ sở dữ liệu PostgreSQL. Mật khẩu và xác thực người dùng được ủy quyền hoàn toàn cho Amazon Cognito.
+ **Phân quyền Quản trị qua Cognito Groups**: Đồng bộ tự động vai trò `ADMIN` giữa ứng dụng NestJS và Cognito User Pool Group `ADMIN`.
+ **Bảo mật Session qua HttpOnly Cookies**: Token xác thực (`sb_access_token`, `sb_id_token`, `sb_refresh_token`) được lưu trong HttpOnly Signed Cookies phía Server, chống lại nguy cơ đánh cắp token qua tấn công XSS.
+ **Kiểm tra Chữ ký JWT với aws-jwt-verify**: NestJS Backend thẩm định trực tiếp chữ ký RSA của token từ Cognito JWKS `us-east-1` đối với mọi request được bảo vệ.
+ **Tự động hóa Lưu trữ Ảnh S3 (`POST /upload`)**: Tích hợp `@aws-sdk/client-s3` cho phép tải ảnh đại diện và logo doanh nghiệp lên S3/MinIO.

#### Nội dung các phần hướng dẫn

1. [Tổng quan về Workshop & Kiến trúc AWS Enterprise](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường, Terraform & Cơ sở dữ liệu PostgreSQL](5.2-Prerequiste/)
3. [Cấu hình Hạ tầng AWS — VPC, RDS, EC2, S3, CloudFront & API Gateway](5.3-AWS-Infrastructure/)
4. [Cấu hình Amazon Cognito User Pool & Confidential App Client](5.4-Cognito-setup/)
5. [Tích hợp Backend NestJS, REST APIs & HttpOnly Cookie Session](5.5-Backend-integration/)
6. [Tích hợp Frontend React 19, Zustand State & Admin Dashboard](5.6-Frontend-integration/)
7. [Tự động hóa Hạ tầng bằng Terraform & Giám sát CloudWatch](5.7-Security-review/)
8. [Dọn dẹp tài nguyên & Tổng kết](5.8-Cleanup/)