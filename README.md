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

## 🧠 Key Learnings

* Difference between:

  * S3 REST endpoint vs Website endpoint
* How CDN works with origin servers
* Configuring public access securely
* Debugging real AWS errors
* Understanding CloudFront ↔ S3 communication

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
