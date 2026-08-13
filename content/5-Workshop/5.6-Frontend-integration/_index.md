---
title: "React Frontend Integration"
date: 2026-08-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

### React 19 Frontend Integration, Zustand State, REST APIs & Admin Dashboard

In this section, we examine how the **React 19 Frontend** application fully integrates with the NestJS Backend REST APIs, manages state using Zustand, and deploys the **Admin Dashboard**.

#### 1. React Frontend Initialization

Open a new Terminal (keep the Backend running) and start the React Frontend:
```bash
cd frontend
npm run dev
```
Navigate to `http://localhost:5173/admin/overview` to view the Admin Dashboard UI. On the **Production** environment, the Admin Dashboard is deployed and accessed via **Amazon CloudFront**, ensuring maximum performance and security.

![Admin Dashboard Production](/images/5-Workshop/5.6-Frontend-integration/admin-dashboard.png)
<p align="center"><i>Figure: Admin Dashboard running on Production — 33 Users, 13 Businesses, 29 Articles, 1 Pending Business</i></p>



#### 2. Auth State & Token Management (`authStore.ts` & Axios Interceptors)
The Frontend leverages **Zustand** store and **Axios Interceptors** to automatically attach the Bearer JWT token to all outbound Backend requests:

```typescript
// Inside services/api.ts
api.interceptors.request.use((config) => {
  const token = useAuthStore.getState().token;
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```

#### 3. Fundraising Form & Backend Write Integration
The "Raise Capital" flow (`PostIdea.tsx`) connects directly to backend write endpoints:
- Create new business (`POST /api/v1/businesses`).
- Post funding opportunity (`POST /api/v1/businesses/:businessId/funding-opportunities`).
- Upload image attachments (`POST /api/v1/upload`).

#### 4. Admin Dashboard Security Guard (`/admin/*`)
The Frontend implements a professional Admin area at the `/admin` route. Access is strictly protected by the **Dual-Layer Authorization Guard** working as follows:
- **Layer 1 — Frontend Guard**: Validates the user's role in the browser before rendering any component.
- **Layer 2 — Backend Guard (`JwtAuthGuard`)**: Every request to `/admin/*` endpoints is verified against the JWT Token and the `ADMIN` role stored in the database.

If a regular `USER` attempts to access the admin route, the system immediately blocks the request and displays **"Admin service is unavailable"**. Only accounts with the `ADMIN` role in the database can access and view the full system statistics.

![Access Denied](/images/5-Workshop/5.6-Frontend-integration/access-denied.png)
<p align="center"><i>Figure: "Access Denied" page displayed when a non-admin user attempts to access the Admin area</i></p>
