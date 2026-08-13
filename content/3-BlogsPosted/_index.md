---
title: "Technical Blogs"
date: 2026-08-12
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# Technical Blogs & Knowledge Sharing Drafts

During the **First Cloud AI Journey (FCAJ)** internship program, three in-depth technical blogs were authored focusing on **AWS Amazon Cognito Cloud Authentication Architecture**, **JWT Cryptographic Signature Verification (`us-east-1`)**, and **HttpOnly Cookie Session Management & RBAC Authorization for Startups Blogs**.

> **Note**: The following articles are technical draft articles prepared to share practical full-stack and cloud implementation experience.

---

### [Blog 1: Building Secure Authentication with Amazon Cognito for React and NestJS Applications](3.1-Blog1/)
Introduces the rationale behind using Amazon Cognito User Pools (`us-east-1`) for centralized identity management, explaining server-side authentication proxying with HMAC-SHA256 `SECRET_HASH`.

### [Blog 2: Securing Amazon Cognito Authentication with SecretHash and JWT RSA Verification in NestJS](3.2-Blog2/)
Focuses on technical implementation details of generating HMAC-SHA256 `SecretHash` and cryptographically verifying RSA signatures using `jwks-rsa` against Cognito JWKS endpoints in `us-east-1`.

### [Blog 3: Managing Sessions with HttpOnly Cookies, Refresh Tokens, and RBAC with Cognito Groups](3.3-Blog3/)
Explores session management using HttpOnly signed cookies to mitigate XSS/CSRF attacks, token renewal flows, and dual-layer authorization combining NestJS RolesGuard with Cognito Group `ADMIN`.