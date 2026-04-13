# Cloud-Native Portfolio & CI/CD Pipeline

A secure, high-performance personal portfolio demonstrating modern DevOps practices and cloud architecture.

## Architecture
The site is hosted on **AWS** and accelerated by **Cloudflare**, utilizing a "Keyless" security model.

* **Storage:** AWS S3 (Static Website Hosting) located in the **af-south-1 (Cape Town)** region.
* **Delivery:** Cloudflare CDN for global edge caching, SSL/TLS termination, and CNAME flattening for the root domain.
* **Security (OIDC):** Instead of storing permanent AWS Access Keys in GitHub, it uses **OpenID Connect (OIDC)**. GitHub Actions assumes a temporary IAM Role.
* **Security (Least Privilege):** The S3 bucket is locked down with a policy that allows traffic *only* from Cloudflare’s IP ranges.

## Stack
* **Development:** Created on **Fedora Linux**.
* **Cloud Provider:** Amazon Web Services.
* **Edge Network:** Cloudflare.
* **CI/CD:** GitHub Actions (YAML).
* **Design:** Custom HTML5/CSS3. (Had a lot of help from AI with this)

## The Pipeline
Every time a change is pushed to the `main` branch, the following automated sequence occurs:

1. **Creation** The changes are first made on my local machine, pushed to my main Codeberg repo, and then mirrored to github
2. **Authentication:** GitHub Actions initiates an OIDC handshake with AWS IAM.
3. **S3 Sync:** The pipeline uses the AWS CLI to sync the repository to the `bremner.me` bucket, ensuring a clean mirror of the code.
4. **Cache Invalidation:** The pipeline sends a secure `POST` request to the Cloudflare API to purge the edge cache. This is done to ensure that updates are visible globally at [https://bremner.me](https://bremner.me) as soon as possible whenever I push an update.

