---
title: "Tích hợp Frontend React"
date: 2026-08-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

### Tích hợp Frontend React 19, Zustand State, REST APIs & Admin Dashboard

Trong phần này, chúng em sẽ xem xét cách ứng dụng **React 19 Frontend** tích hợp toàn diện với NestJS Backend REST APIs, quản lý trạng thái bằng Zustand, và triển khai giao diện **Admin Dashboard**.

#### 1. Khởi chạy Frontend React và Truy cập Admin Dashboard

Bạn cần giữ nguyên cửa sổ Terminal đang chạy Backend, và mở một Terminal mới để khởi chạy giao diện Frontend:
```bash
cd frontend
npm run dev
```
Sau đó, truy cập vào trình duyệt tại địa chỉ: `http://localhost:5173/admin/overview`. Trên môi trường **Production**, Admin Dashboard được triển khai và truy cập thông qua **Amazon CloudFront**, đảm bảo hiệu năng và bảo mật cao nhất.

![Admin Dashboard Production](/images/5-Workshop/5.6-Frontend-integration/admin-dashboard.png)
<p align="center"><i>Hình: Admin Dashboard đang hoạt động trên Production — 33 Users, 13 Businesses, 29 Articles, 1 Pending Business</i></p>


#### 2. Quản lý Trạng thái Xác thực & Token (`authStore.ts` & Axios Interceptors)
Frontend sử dụng thư viện **Zustand** kết hợp với **Axios Interceptors** để tự động đính kèm Bearer JWT Token vào mọi API request gửi lên Backend:

```typescript
// Trong services/api.ts
api.interceptors.request.use((config) => {
  const token = useAuthStore.getState().token;
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```

#### 3. Tích hợp Luồng Đăng ký Gọi vốn & Backend Write APIs
Giao diện Đăng ký Gọi vốn (`PostIdea.tsx` / `RaiseCapital`) kết nối trực tiếp với backend write endpoints:
- Đăng tạo doanh nghiệp mới (`POST /api/v1/businesses`).
- Đăng tải tin gọi vốn (`POST /api/v1/businesses/:businessId/funding-opportunities`).
- Tải tệp hình ảnh đính kèm (`POST /api/v1/upload`).

#### 4. Bảo mật Giao diện Quản trị viên (Admin Dashboard Guard)
Hệ thống Frontend triển khai khu vực Admin chuyên nghiệp tại tuyến đường `/admin`. Khu vực này được bảo vệ nghiêm ngặt bởi **Dual-Layer Authorization Guard** hoạt động theo cơ chế:
- **Tầng 1 — Frontend Guard**: Kiểm tra vai trò người dùng ngay tại trình duyệt trước khi render bất kỳ component nào.
- **Tầng 2 — Backend Guard (`JwtAuthGuard`)**: Mỗi request đến endpoint `/admin/*` đều được Backend xác thực JWT Token và kiểm tra vai trò `ADMIN` trong cơ sở dữ liệu.

Nếu một tài khoản `USER` thông thường cố tình truy cập vào đường dẫn quản trị, hệ thống sẽ lập tức chặn và hiển thị thông báo **"Admin service is unavailable"**. Chỉ tài khoản có vai trò `ADMIN` trong database mới có thể truy cập và xem toàn bộ số liệu thống kê hệ thống.

![Access Denied](/images/5-Workshop/5.6-Frontend-integration/access-denied.png)
<p align="center"><i>Hình: Trang "Access Denied" hiển thị khi người dùng không có quyền truy cập khu vực Admin</i></p>

