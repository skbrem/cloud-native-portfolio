# Cloud-Native Portfolio & CI/CD Pipeline

This repository hosts my personal portfolio, serving as a hands-on demonstration of Cloud Engineering and DevOps principles. It features a serverless architecture optimized for the **af-south-1 (Cape Town)** region, delivered globally via **Cloudflare**.

## 🏗️ Architecture Overview

The project follows a "Keyless" security model, utilizing **Identity Federation** between GitHub and AWS to eliminate the need for long-lived IAM credentials.

```mermaid
graph LR
    A[Local Fedora Dev] -- git push --> B(GitHub Repository)
    subgraph GitHub Actions
    B --> C{OIDC Auth}
    C -- Temporary Token --> D[AWS IAM Role]
    D --> E[S3 Sync]
    E --> F[Cloudflare Purge]
    end
    subgraph AWS (af-south-1)
    E --> G[(S3 Bucket: bremner.me)]
    end
    subgraph Edge Network
    F --> H[Cloudflare Edge Cache]
    G -.-> H
    H --> I((End User))
    end

