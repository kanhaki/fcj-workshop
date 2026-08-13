---
title: "Các bài blogs đã đăng"
date: 2026-08-12
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# Danh sách các Bài viết Kỹ thuật (Technical Blogs Drafts)

Trong quá trình nghiên cứu và thực tập tại chương trình **First Cloud AI Journey (FCAJ)**, em đã biên soạn 3 bài viết kỹ thuật chuyên sâu xoay quanh chủ đề **Kiến trúc Xác thực Đám mây AWS Amazon Cognito**, **Bảo mật JWT Token với aws-jwt-verify (`us-east-1`)**, và **Quản lý Session qua HttpOnly Cookie & Phân quyền RBAC cho ứng dụng Startups Blogs**.

> **Ghi chú**: Các bài viết kỹ thuật dưới đây là bản dự thảo kỹ thuật (Drafts) được chuẩn bị để chia sẻ kinh nghiệm thực tế.

---

### [Blog 1: Xây dựng Hệ thống Xác thực Bảo mật với Amazon Cognito cho Ứng dụng React và NestJS](3.1-Blog1/)
Bài viết giới thiệu tổng quan về lý do lựa chọn Amazon Cognito User Pool (`us-east-1`) làm giải pháp quản lý danh tính tập trung cho nền tảng Startups Blogs, lý do không lưu mật khẩu trực tiếp ở cơ sở dữ liệu nội bộ và kiến trúc gửi request xác thực qua NestJS Server-side với `SECRET_HASH` (HMAC-SHA256).

### [Blog 2: Bảo mật Xác thực Amazon Cognito với SecretHash và Kiểm tra Chữ ký JWT qua JWKS trong NestJS](3.2-Blog2/)
Bài viết đi sâu vào cơ chế kỹ thuật sinh mã `SecretHash` HMAC-SHA256 từ `COGNITO_CLIENT_SECRET`, quy trình thẩm định token trực tiếp qua `jwks-rsa` / `aws-jwt-verify` với RSA Public Keys từ JWKS `us-east-1`, và tại sao chỉ decode JWT đơn thuần là chưa đủ an toàn.

### [Blog 3: Quản lý Phiên Đăng nhập bằng HttpOnly Cookie, Refresh Token và Phân quyền RBAC kết hợp Cognito Groups](3.3-Blog3/)
Bài viết phân tích phương án lưu trữ JWT trong HttpOnly Signed Cookie chống tấn công XSS/CSRF, quy trình cấp lại token với Refresh Token, và cơ chế phân quyền hai tầng kết hợp giữa NestJS RolesGuard và Cognito User Pool Group `ADMIN`.