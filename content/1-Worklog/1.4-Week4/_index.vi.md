---
title: "Worklog Tuần 4"
date: 2026-07-13
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

- Tích hợp giao diện Frontend với luồng xác thực Amazon Cognito Auth (Đăng nhập, Đăng ký, Xác thực Email OTP).
- Tìm hiểu dịch vụ Amazon Cognito User Pools và cấu hình Confidential Client.
- Quản lý trạng thái xác thực bằng Zustand store (`authStore`).
- Điều tra và xử lý sự cố vỡ giao diện thẻ hình ảnh (`<img>`) khi trình duyệt bật tính năng Google Chrome Translate.
- Kiểm thử luồng đăng nhập và trải nghiệm người dùng trên giao diện.

### Công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Xây dựng giao diện Đăng ký tài khoản (`Register.tsx`) <br> - Lập trình form chọn vai trò (`BUSINESS_OWNER`, `INVESTOR`, `ENTERPRISE_PARTNER`) | 13/07/2026 | 13/07/2026 | |
| 2 | - Lập trình giao diện Đăng nhập (`Login.tsx`) và Quên mật khẩu (`ForgotPassword.tsx`) <br> - Xây dựng màn hình nhập mã xác thực OTP 6 chữ số (`PendingVerification.tsx`) <br> - Tìm hiểu kiến thức cơ bản về Amazon Cognito User Pools | 14/07/2026 | 14/07/2026 | <https://docs.aws.amazon.com/cognito/> |
| 3 | - Kết nối các form auth với Backend REST API xác thực Amazon Cognito <br> - Sử dụng Zustand (`authStore`) để quản lý token và thông tin phiên người dùng trên Frontend | 15/07/2026 | 15/07/2026 | <https://github.com/pmndrs/zustand> |
| 4 | - Điều tra nguyên nhân gây vỡ giao diện thẻ ảnh khi trình duyệt bật Chrome Translate <br> - Phân tích cơ chế Chrome Translate tự động bọc node văn bản làm sai lệch cấu trúc DOM React | 16/07/2026 | 16/07/2026 | |
| 5 | - Áp dụng các giải pháp bảo vệ thẻ DOM `<img>` chống đột biến từ trình dịch <br> - Kiểm thử toàn bộ luồng đăng ký, xác thực OTP và đăng nhập Cognito mượt mà trên giao diện | 17/07/2026 | 17/07/2026 | |


### Kết quả đạt được tuần 4:

- Tích hợp thành công giao diện với các luồng xác thực Amazon Cognito Auth.
- Hiểu tổng quan cơ chế xác thực danh tính người dùng bằng Amazon Cognito User Pool.
- Quản lý hiệu quả trạng thái phiên làm việc người dùng bằng Zustand store (`authStore`).
- Giải quyết triệt để sự cố vỡ giao diện thẻ hình ảnh do tính năng Chrome Translate.
- Đảm bảo luồng đăng ký, xác thực OTP 6 chữ số và đăng nhập hoạt động an toàn, liền mạch.
