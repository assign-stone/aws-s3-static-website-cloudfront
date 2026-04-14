# 🌐 AWS S3 Static Website Hosting with CloudFront

This project demonstrates how to deploy a static website using AWS services with HTTPS and CDN optimization.

---

## 🚀 Project Overview

In this project, I built and deployed a static portfolio website using:

* Amazon S3 (for hosting)
* Amazon CloudFront (for CDN + HTTPS)
* HTML5, CSS3 for frontend

---

## 🏗️ Architecture

User → CloudFront (CDN + HTTPS) → S3 (Static Website Hosting)

---

## 🛠️ Technologies Used

* AWS S3
* AWS CloudFront
* HTML5
* CSS3

---

## 📂 Project Structure

```
.
├── index.html
├── style.css
└── images/
    └── hero.svg
```

---

## ⚙️ Step-by-Step Implementation

### 1️⃣ Create S3 Bucket

* Created a bucket in AWS S3
* Selected region (ap-south-1)
* Disabled **Block all public access**
* Selected **SSE-S3 encryption (default)**

---

### 2️⃣ Upload Website Files

* Uploaded:

  * index.html
  * style.css
  * images folder

---

### 3️⃣ Enable Static Website Hosting

* Enabled static website hosting in bucket properties
* Set:

  * Index document → `index.html`
* Copied S3 website endpoint

---

### 4️⃣ Configure Public Access (Bucket Policy)

Added the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

---

### 5️⃣ Create CloudFront Distribution

* Created distribution in AWS CloudFront
* Selected **Free plan**
* Added S3 as origin

---

### 6️⃣ Configure Origin (IMPORTANT)

* Used **S3 Website Endpoint**:

```
your-bucket-name.s3-website-ap-south-1.amazonaws.com
```

* Set:

  * Origin protocol policy → **HTTP only**
* Disabled:

  * Private bucket access (OAC)

---

### 7️⃣ Configure Cache & Security

* Used recommended cache settings
* Left WAF default (no changes)

---

### 8️⃣ Deploy CloudFront

* Created distribution
* Waited for status → **Deployed**
* Accessed site using:

```
https://your-cloudfront-url
```

---

### 9️⃣ Enable HTTPS Redirect

* Edited CloudFront behavior
* Set:

  * Viewer protocol policy → **Redirect HTTP to HTTPS**

---

## ❗ Challenges Faced & Fixes

### ❌ Access Denied Error

* **Cause:** Used S3 REST endpoint
* **Fix:** Switched to S3 website endpoint

---

### ❌ Failed to Contact Origin

* **Cause:** HTTPS between CloudFront and S3
* **Fix:** Changed origin protocol to HTTP only

---

### ❌ CSS / Images Not Loading

* **Cause:** Incorrect file structure
* **Fix:** Uploaded files at root level

---

## ⚠️ Important Note on Resource Cleanup (CloudFront Plan Issue)

While deleting resources after completing this project, I encountered a limitation with Amazon CloudFront’s new plan-based pricing model.

### 🔴 Issue Faced

When attempting to delete the CloudFront distribution, the following error occurred:

> *"You can't delete this distribution while it's subscribed to a pricing plan. After you cancel the pricing plan, you can delete the distribution at the end of monthly billing cycle."*

---

### 🧠 Root Cause

* The CloudFront distribution was subscribed to the **Free Plan ($0/month)**.
* Even after cancelling the plan, AWS keeps the subscription active until the **end of the billing cycle**.
* During this period, the distribution **cannot be deleted immediately**.

---

### ✅ Solution / Workaround

To avoid any unnecessary charges:

1. **Disabled the CloudFront distribution**

   * This stops all traffic and usage.

2. **Deleted the S3 bucket (origin)**

   * Ensures no data transfer occurs.

3. **Cancelled the CloudFront plan**

   * Prevents future billing.

---

### 💰 Cost Impact

* CloudFront charges are based on:

  * Data transfer
  * Number of requests

* Since:

  * No origin (S3 deleted)
  * No traffic
  * Usage = 0%

👉 **No additional cost is incurred during the waiting period.**

---

### 📌 Key Takeaway

> In AWS, some services (like CloudFront with plans) may restrict immediate deletion due to billing lifecycle constraints.
> Always disable resources and stop traffic first to ensure cost safety.

---

## 🧠 Key Learnings

* Difference between:

  * S3 REST endpoint vs Website endpoint
* How CDN works with origin servers
* Configuring public access securely
* Debugging real AWS errors
* Understanding CloudFront ↔ S3 communication
* Understood AWS billing lifecycle behavior
* Learned how CloudFront plan-based restrictions work
* Practiced safe resource cleanup strategies
---

## 🌍 Live Demo

CloudFront URL:
👉 https://your-cloudfront-url

---

## 💡 Future Improvements

* Add custom domain using AWS Route 53
* Implement CI/CD pipeline
* Add monitoring using CloudWatch
* Convert to React-based frontend

---

## 👩‍💻 Author

Shivani Joshi

---
