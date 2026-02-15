# AWS Edge-Optimized Portfolio 🚀

A high-performance, secure static website hosted on AWS using a serverless architecture. This project demonstrates Infrastructure as Code (IaC) principles and the AWS Well-Architected Framework.

## 🏗️ Architecture
- **Storage:** Amazon S3 (Private Bucket)
- **Content Delivery:** Amazon CloudFront (CDN)
- **Security:** Origin Access Control (OAC) & AWS Certificate Manager (SSL/TLS)
- **DNS:** Amazon Route 53

## 🛡️ Key Features
* **Least Privilege Security:** The S3 bucket is strictly private. Access is granted only to CloudFront via **Origin Access Control (OAC)**, preventing direct S3 URL access.
* **Global Latency Reduction:** Content is cached at over 600+ Edge Locations globally.
* **Automated Deployment:** Includes a Bash script for syncing local builds from Fedora to S3 and invalidating the CloudFront cache.

## 🚀 Deployment (Fedora/Linux)
To deploy updates from your local machine:

1. **Prerequisites:** AWS CLI configured with appropriate IAM permissions.
2. **Sync Files:**
   ```bash
   aws s3 sync ./src s3://your-bucket-name --delete
