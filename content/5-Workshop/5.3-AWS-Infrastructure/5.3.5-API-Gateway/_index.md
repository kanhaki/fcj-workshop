---
title: "API Gateway"
date: 2026-08-01
weight: 5
chapter: false
pre: " <b> 5.3.5 </b> "
---

### Amazon API Gateway Setup

#### Step 1 — Create HTTP API

Go to **AWS Console** → **API Gateway** → click **Create API**.

Select **HTTP API** → click **Build**.

Fill in:
- **API name**: `startups-blogs-api`

Click **Next** → **Next** → **Create**.

![Step 1 - Create HTTP API](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step1-create-api.png)
<p align="center"><i>Figure: Create HTTP API named startups-blogs-api</i></p>

---

#### Step 2 — Create Integration with EC2 Backend

On the left menu, select **Integrations** → **Manage integrations** → **Create**.

Configure:
- **Integration type**: HTTP URI
- **HTTP method**: ANY
- **URL endpoint**: `http://EC2_PUBLIC_IP:3000/{proxy}`

Click **Create**.

![Step 2 - Create Integration](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step2-integration.png)
<p align="center"><i>Figure: Integration pointing to EC2 Backend at port 3000</i></p>

---

#### Step 3 — Create Proxy Route

On the left menu, select **Routes** → **Create**.

Configure:
- **Method**: `ANY`
- **Path**: `/{proxy+}`
- **Integration target**: Select the integration created in Step 2

Click **Create**.

![Step 3 - Create Route](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step3-route.png)
<p align="center"><i>Figure: ANY /{proxy+} route forwarding all requests to the Backend</i></p>

---

#### Step 4 — Configure CORS

On the left menu, select **CORS** → **Configure**.

Fill in:
- **Access-Control-Allow-Origin**: `*`
- **Access-Control-Allow-Methods**: `GET, POST, PUT, DELETE, OPTIONS, PATCH`
- **Access-Control-Allow-Headers**: `*`

Click **Save**.

![Step 4 - CORS Configuration](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step4-cors.png)
<p align="center"><i>Figure: CORS configuration allowing the Frontend to call the API</i></p>

---

#### Step 5 — Get Invoke URL and Update Frontend

Go to **Stages** → select the `$default` stage → copy the **Invoke URL**.

```
https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com
```

Update the environment variable in the Frontend:
```env
# frontend/.env.production
VITE_API_URL=https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com
```

Rebuild the Frontend and upload to S3:
```bash
npm run build
aws s3 sync dist/ s3://startups-blogs-frontend --delete
```

![Step 5 - Invoke URL](/images/5-Workshop/5.3-AWS-Infrastructure/5.3.5-step5-invoke-url.png)
<p align="center"><i>Figure: API Gateway Invoke URL used by the Frontend</i></p>
