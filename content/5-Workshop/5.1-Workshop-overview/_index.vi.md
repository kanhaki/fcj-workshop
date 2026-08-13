---
title: "Tổng quan Workshop"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Tổng quan bài lab & Kiến trúc Đám mây AWS Enterprise

Trong bài hướng dẫn này, chúng em sẽ tìm hiểu kiến trúc tổng thể của hệ thống **Startups Blogs** và luồng xác thực đám mây bằng **Amazon Cognito (`us-east-1`)**.

#### 1. Sơ đồ Kiến trúc AWS Enterprise
Hệ thống được thiết kế theo chuẩn Enterprise Microservices & Serverless kết hợp, tách biệt hoàn toàn giữa Frontend, Backend, Database và Hệ thống Xác thực. Toàn bộ hạ tầng được tự động hóa bằng **Terraform** (Infrastructure as Code).

![Sơ đồ kiến trúc hệ thống Startups Blogs](/images/5-Workshop/5.1-Workshop-overview/AWS%20Architect.drawio.png)
<p align="center"><i>Hình: Sơ đồ kiến trúc hệ thống Startups Blogs</i></p>

#### 2. Phân định rõ các vai trò và phạm vi đăng ký
Hệ thống quản lý 4 vai trò người dùng chính (`UserRole`):
- **`BUSINESS_OWNER`**: Đăng ký công khai. Tạo và quản lý hồ sơ doanh nghiệp, công bố tin gọi vốn.
- **`INVESTOR`**: Đăng ký công khai. Tìm kiếm, tra cứu và đánh giá các cơ hội đầu tư.
- **`ENTERPRISE_PARTNER`**: Đăng ký công khai. Tham gia hợp tác chiến lược và đồng đầu tư.
- **`ADMIN`**: **Không mở đăng ký công khai**. Đồng bộ tự động với Cognito User Pool Group `ADMIN` qua `CognitoGroupsService`. Quản trị viên sử dụng Admin Dashboard để phê duyệt doanh nghiệp (`PUT /businesses/admin/:id/status`), kiểm duyệt bài viết và tạo Đề xuất thay đổi (`ChangeProposal`).

#### 3. Phân định tính năng Thực tế (Implemented) vs Tương lai (Planned)
- **ĐÃ TRIỂN KHAI VÀ KIỂM THỬ (IMPLEMENTED AND VERIFIED)**:
  - Hạ tầng mã nguồn Terraform IaC tại `terraform/` (Region: `us-east-1`).
  - Cơ sở dữ liệu Amazon RDS PostgreSQL & Prisma ORM Schema đầy đủ.
  - REST APIs Đọc & Ghi Doanh nghiệp (`POST/GET/PUT/DELETE /businesses`).
  - REST APIs Đăng tin Gọi vốn (`POST/GET/PUT/DELETE /businesses/:businessId/funding-opportunities`).
  - Tải ảnh đính kèm lên S3/MinIO (`POST /upload`).
  - Backend xác thực Amazon Cognito, SecretHash HMAC-SHA256, và đồng bộ Cognito Group `ADMIN`.
  - Bảo mật HttpOnly Signed Cookie & kiểm tra chữ ký RSA Token qua `aws-jwt-verify` từ JWKS `us-east-1`.
  - Giao diện React 19 Frontend, AuthStore Zustand, Admin Dashboard (`/admin/*`) và Đề xuất thay đổi (Change Proposals).
  - Yêu cầu liên hệ (`POST /businesses/:businessId/contact-requests`).
- **DỰ KIẾN TƯƠNG LAI (PLANNED)**:
  - Hệ thống Thông báo thời gian thực (Real-time Notification System với Notification Schema & WebSocket).
  - Tối ưu hóa luồng phê duyệt gọi vốn đa tầng.
  - Mở rộng bộ kiểm thử tự động E2E.

#### 4. Giao diện ứng dụng Startups Blogs

Dưới đây là một số hình ảnh thực tế về giao diện của ứng dụng web Startups Blogs sau khi triển khai thành công:

**Trang chủ (Phần Đầu):** Giao diện Header trực quan, hiển thị các tính năng cốt lõi và thanh điều hướng chính của nền tảng.
![Giao diện Header Trang chủ](/images/5-Workshop/5.1-Workshop-overview/home-page%20(1).png)
<p align="center"><i>Hình: Giao diện Header Trang chủ</i></p>

**Trang chủ (Phần Nội dung):** Danh sách các Startups, cơ hội đầu tư nổi bật và các bài viết mới nhất được tải từ Backend thông qua API.
![Giao diện Nội dung Trang chủ](/images/5-Workshop/5.1-Workshop-overview/home-page%20(2).png)
<p align="center"><i>Hình: Giao diện Nội dung Trang chủ</i></p>

**Sơ đồ Thực thể Liên kết (ERD):** Sơ đồ mô tả cấu trúc cơ sở dữ liệu PostgreSQL của hệ thống, bao gồm các bảng `users`, `businesses`, `articles` và các mối quan hệ (owns, writes, v.v.).
![Sơ đồ Thực thể Liên kết (ERD)](/images/5-Workshop/5.1-Workshop-overview/Business%20Funding-2026-08-13-081827.png)
<p align="center"><i>Hình: Sơ đồ Thực thể Liên kết (ERD) của hệ thống</i></p>

