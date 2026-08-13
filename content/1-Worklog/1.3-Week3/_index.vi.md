---
title: "Worklog Tuần 3"
date: 2026-07-06
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

- Phát triển giao diện trang cá nhân người dùng (`UserProfile.tsx`).
- Xây dựng giao diện bảng điều khiển người dùng (User Dashboard).
- Tìm hiểu khái niệm lưu trữ cơ sở dữ liệu quan hệ trong dịch vụ Amazon RDS cho PostgreSQL.
- Gọi API backend để hiển thị thông tin chi tiết người dùng (`GET /users/me`, `GET /users/:id`).
- Xử lý binding dữ liệu tĩnh và động lên UI cá nhân.

### Công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | - Thiết kế bố cục giao diện Trang cá nhân người dùng (UserProfile Page) <br> - Lập trình khung hiển thị avatar, bio, thông tin liên hệ và số lượng người theo dõi | 06/07/2026 | 06/07/2026 | |
| 2 | - Xây dựng giao diện Bảng điều khiển người dùng (User Dashboard) <br> - Lập trình các tab quản lý bài viết đã đăng và danh sách doanh nghiệp sở hữu | 07/07/2026 | 07/07/2026 | |
| 3 | - Tìm hiểu tổng quan về dịch vụ Amazon RDS và cơ sở dữ liệu quan hệ PostgreSQL <br> - Viết các hàm API service kết nối endpoint `GET /users/me` và `GET /users/:id` | 08/07/2026 | 08/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Thực hiện ghép nối API với giao diện UserProfile và Dashboard <br> - Binding dữ liệu động từ backend lên các thẻ UI hiển thị thông tin cá nhân | 09/07/2026 | 09/07/2026 | |
| 5 | - Kiểm thử hiển thị thông tin profile người dùng trên trình duyệt <br> - Xử lý ngoại lệ dữ liệu khi người dùng chưa đăng nhập hoặc profile không tồn tại | 10/07/2026 | 10/07/2026 | |


### Kết quả đạt được tuần 3:

- Hoàn thành giao diện Trang cá nhân (UserProfile) và Bảng điều khiển (User Dashboard).
- Nắm vững vai trò lưu trữ dữ liệu người dùng và doanh nghiệp trong cơ sở dữ liệu PostgreSQL.
- Tích hợp thành công API service kết nối lấy dữ liệu profile người dùng từ Backend.
- Hiển thị đầy đủ và chính xác thông tin cá nhân, danh mục bài viết và doanh nghiệp sở hữu.
- Xử lý mượt mà các trường hợp ngoại lệ dữ liệu trên giao diện.
