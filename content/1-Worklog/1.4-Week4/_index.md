---
title: "Week 4 Worklog"
date: 2026-07-13
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Week 4 Objectives:

- Integrate Frontend UI components with Amazon Cognito Auth flows (Login, Register, Email OTP Verification).
- Study Amazon Cognito User Pools and Confidential Client integration concepts.
- Manage global authentication state using Zustand store (`authStore`).
- Investigate and resolve UI image card rendering glitches caused by Google Chrome Translate DOM mutations.
- Test authentication flows and overall user experience on the frontend.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Built the Registration UI (`Register.tsx`) <br> - Implemented role selection form controls (`BUSINESS_OWNER`, `INVESTOR`, `ENTERPRISE_PARTNER`) | 13/07/2026 | 13/07/2026 | |
| 2 | - Developed Login UI (`Login.tsx`) and Forgot Password view (`ForgotPassword.tsx`) <br> - Constructed the 6-digit Email OTP Verification view (`PendingVerification.tsx`) <br> - Studied Amazon Cognito User Pools architecture fundamentals | 14/07/2026 | 14/07/2026 | <https://docs.aws.amazon.com/cognito/> |
| 3 | - Connected authentication forms to backend REST APIs powered by Amazon Cognito <br> - Utilized Zustand (`authStore`) for managing tokens and session user state | 15/07/2026 | 15/07/2026 | <https://github.com/pmndrs/zustand> |
| 4 | - Investigated DOM rendering issues affecting image cards under Google Chrome Translate <br> - Analyzed Chrome Translate text-node wrapping behaviors causing React DOM mismatches | 16/07/2026 | 16/07/2026 | |
| 5 | - Implemented DOM node protection attributes on image elements to prevent translate crashes <br> - Tested end-to-end user registration, OTP verification, and Cognito login | 17/07/2026 | 17/07/2026 | |


### Week 4 Achievements:

- Successfully integrated Frontend UI components with Amazon Cognito Auth workflows.
- Understood user identity authentication mechanisms using Amazon Cognito User Pools.
- Effectively managed user session states via Zustand store (`authStore`).
- Resolved image card rendering issues caused by Chrome Translate DOM mutations.
- Ensured registration, 6-digit OTP confirmation, and login flows operate smoothly and securely.
