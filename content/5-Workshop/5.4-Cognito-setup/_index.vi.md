---
title: "Cấu hình Amazon Cognito"
date: 2026-08-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Cấu hình Amazon Cognito User Pool, App Client & Cognito Groups (`us-east-1`)

Trong phần này, chúng em sẽ quản lý danh tính người dùng bảo mật cho nền tảng Startups Blogs qua **Amazon Cognito User Pool** tại Region **`us-east-1`**.

#### 1. Tổng quan các bước cấu hình Cognito sơ bộ
Trong hệ thống Startups Blogs, toàn bộ các chính sách bảo mật cốt lõi của Cognito đã được cấu hình với các tiêu chuẩn sau:
- **Sign-in experience**: Cho phép người dùng đăng nhập trực tiếp bằng `Email`.
- **Password policy**: Yêu cầu mật khẩu mạnh (tối thiểu 8 ký tự, bao gồm chữ hoa, chữ thường, số và ký tự đặc biệt).
- **Email verification**: Hệ thống tự động gửi mã xác thực (Verification Code) qua email khi người dùng đăng ký tài khoản mới.
- **App Client Security**: Tích hợp luồng xác thực **SecretHash HMAC-SHA256**. Backend NestJS sẽ tính toán mã Hash dựa trên `ClientId` và `ClientSecret` trước khi gọi các API của Cognito, đảm bảo độ bảo mật tuyệt đối cho kiến trúc Microservices.

#### 2. Quản lý Người dùng (Users)
Xem và quản lý các tài khoản đã đăng ký trong Cognito User Pool.
1. Truy cập vào User Pool của bạn trên **Amazon Cognito** (Region `us-east-1`).
2. Ở menu bên trái, chọn **User management > Users**.
3. Tại đây, bạn có thể kiểm tra danh sách tài khoản, trạng thái xác thực email và trạng thái hoạt động.

![Cognito Users](/images/5-Workshop/5.4-Cognito-setup/users.png)
<p align="center"><i>Hình: Cognito Users</i></p>

#### 3. Cấu hình Cognito Groups cho Vai trò ADMIN
Tạo một Cognito User Pool Group tên là **`ADMIN`**. Ở menu bên trái, chọn **User management > Groups** để xem nhóm `ADMIN` và các thành viên đã được cấp quyền.

Vai trò `ADMIN` trong hệ thống NestJS được đồng bộ tự động với nhóm `ADMIN` này thông qua `CognitoGroupsService` bằng các lệnh AWS SDK:
- `AdminAddUserToGroupCommand`
- `AdminRemoveUserFromGroupCommand`

```typescript
// Trong cognito-groups.service.ts
const command = isAdmin
  ? new AdminAddUserToGroupCommand({ GroupName: 'ADMIN', Username: username, UserPoolId: userPoolId })
  : new AdminRemoveUserFromGroupCommand({ GroupName: 'ADMIN', Username: username, UserPoolId: userPoolId });
await this.client.send(command);
```

![Cognito ADMIN Group](/images/5-Workshop/5.4-Cognito-setup/group-admin.png)
<p align="center"><i>Hình: Cognito ADMIN Group</i></p>

#### 4. Cấu hình App Client & Authentication Flows
1. Ở menu bên trái, chọn **Applications > App clients**.
2. Nhấn vào tên App Client của bạn (ví dụ: `startups-blogs-app`).
3. Dưới mục **App client information**, kiểm tra lại **Client ID**.
4. Dưới mục **Authentication flows**, đảm bảo các luồng như **Username and password** và **Secure remote password (SRP)** được bật.

![Cognito App Client Settings](/images/5-Workshop/5.4-Cognito-setup/app-client.png)
<p align="center"><i>Hình: Cognito App Client Settings</i></p>

#### 5. Tham số Cấu hình Môi trường Backend
Ghi nhận các tham số để cấu hình file `.env` phía Backend NestJS (chú ý **không bao giờ commit file `.env` chứa secret lên Git**):

```env
AWS_REGION=us-east-1
COGNITO_USER_POOL_ID=us-east-1_xxxxxxxxx
COGNITO_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxx
COGNITO_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

![Cognito User Pool Overview](/images/5-Workshop/5.4-Cognito-setup/overview.png)
<p align="center"><i>Hình: Cognito User Pool Overview</i></p>

