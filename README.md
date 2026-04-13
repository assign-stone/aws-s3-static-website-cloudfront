# 🌐 AWS S3 Static Website Hosting with CloudFront

This project demonstrates how to deploy a static website using AWS services with HTTPS and CDN optimization.

---

## 🚀 Project Overview

In this project, I built and deployed a static portfolio website using:

- Amazon S3 (for hosting)
- Amazon CloudFront (for CDN + HTTPS)
- Basic HTML, CSS for frontend

---

## 🏗️ Architecture

User → CloudFront (CDN + HTTPS) → S3 (Static Website Hosting)

---

## 🛠️ Technologies Used

- AWS S3
- AWS CloudFront
- HTML5
- CSS3

---

## 📂 Project Structure
.
├── index.html
├── style.css
└── images/
└── hero.svg


---

## ⚙️ Step-by-Step Implementation

### 1. Created S3 Bucket
- Created a bucket in AWS S3
- Disabled "Block all public access"
- Enabled static website hosting

---

### 2. Uploaded Website Files
- Uploaded:
  - index.html
  - style.css
  - images folder

---

### 3. Enabled Static Website Hosting
- Set index document as `index.html`
- Got S3 website endpoint

---

### 4. Configured Bucket Policy
Allowed public read access using:

```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::your-bucket-name/*"
}

5. Created CloudFront Distribution
Selected S3 as origin
Used S3 website endpoint
Set origin protocol policy to HTTP only

6. Enabled HTTPS
Used CloudFront default SSL
Accessed site via HTTPS

7. Fixed Errors
❌ Access Denied
Cause: Wrong origin (S3 REST endpoint)
Fix: Switched to S3 website endpoint
❌ Failed to Contact Origin
Cause: HTTPS used between CloudFront and S3
Fix: Changed to HTTP only


🧠 Key Learnings
Difference between S3 REST endpoint vs Website endpoint
How CDN works with origin servers
Configuring public access securely
Debugging real AWS errors
💡 Future Improvements
Add custom domain using Route 53
Implement CI/CD pipeline
Add monitoring with CloudWatch



👩‍💻 Author
Shivani Joshi
