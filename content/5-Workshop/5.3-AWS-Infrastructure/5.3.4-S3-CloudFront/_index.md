---
title: "S3 Bucket & CloudFront"
date: 2026-08-01
weight: 4
chapter: false
pre: " <b> 5.3.4 </b> "
---

### S3 Bucket & CloudFront Distribution Setup

#### Step 1 — Create S3 Bucket for Media

Go to **AWS Console** → **S3** → **Create bucket**.

Fill in the information:
- **Bucket name**: `startups-blogs-media`
- **Region**: `us-east-1`
- **Block Public Access**: Uncheck *"Block all public access"* → acknowledge the warning

Click **Create bucket**.

![Step 1 - Create Media Bucket](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step1-media-bucket.png)
<p align="center"><i>Figure: Create S3 Bucket for Media with Public Access</i></p>

---

#### Step 2 — Configure CORS for Media Bucket

Go to the `startups-blogs-media` bucket → **Permissions** tab → scroll down to **Cross-origin resource sharing (CORS)** → click **Edit**.

Paste the following JSON:
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": []
  }
]
```

Click **Save changes**.

![Step 2 - CORS Configuration](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step2-cors.png)
<p align="center"><i>Figure: CORS configuration allowing Frontend to upload images</i></p>

---

#### Step 3 — Create S3 Bucket for Frontend

Create a second bucket:
- **Bucket name**: `startups-blogs-frontend`
- **Region**: `us-east-1`
- **Block Public Access**: Keep default (CloudFront will manage access)

After creating, go to **Properties** → scroll down to **Static website hosting** → **Edit**:
- **Enable** Static website hosting
- **Index document**: `index.html`
- **Error document**: `index.html`

![Step 3 - Static Website Hosting](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step3-static-hosting.png)
<p align="center"><i>Figure: Enable Static Website Hosting for Frontend Bucket</i></p>

---

#### Step 4 — Upload Frontend to S3

Build the Frontend and upload:
```bash
cd frontend
npm run build
aws s3 sync dist/ s3://startups-blogs-frontend --delete
```

---

#### Step 5 — Create CloudFront Distribution

Go to **CloudFront** → **Create distribution**.

Configure:
- **Origin domain**: Select the `startups-blogs-frontend` bucket
- **Origin access**: **Origin access control (OAC)** → Create new OAC
- **Default root object**: `index.html`

![Step 5 - Create Distribution](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step5-distribution.png)
<p align="center"><i>Figure: Configure Origin for CloudFront Distribution</i></p>

---

#### Step 6 — Configure Error Pages and Deploy

In the **Error pages** tab → **Create custom error response**:
Create two custom error responses (for 403 and 404):
- **HTTP error code**: 403 (and 404 for the second one)
- **Response page path**: `/index.html`
- **HTTP response code**: 200

*(This step ensures React Router works correctly when the page is refreshed or a path is not found)*

Click **Create distribution** → wait for the status to become **Enabled** (takes about 5 minutes).

Note down the **Distribution domain name**: `xxxxxxxx.cloudfront.net`

![Step 6 - CloudFront Enabled](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.4-step6-enabled.png)
<p align="center"><i>Figure: CloudFront Distribution is active with a domain name</i></p>
