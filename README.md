# Cloud-Native Portfolio 

A high-performance, secure static website hosted on AWS using a serverless architecture. This project serves as my professional portfolio and demonstrates hands-on experience with Infrastructure as Code (IaC) and CI/CD pipelines.

## Architecture

* **Storage:** Amazon S3 (af-south-1 / Cape Town Region) - Strictly private bucket
* **Content Delivery:** Amazon CloudFront (CDN)
* **Security:** Origin Access Control (OAC) & AWS Certificate Manager (SSL/TLS)
* **DNS:** Amazon Route 53

## Key Features

* **Least Privilege Security:** The S3 bucket is strictly private. Access is granted only to CloudFront via **Origin Access Control (OAC)**, preventing direct S3 URL access.
* **Global Latency Reduction:** Content is cached at over 600+ Edge Locations globally.

## CI/CD Pipeline

This project utilizes a fully automated CI/CD pipeline:
1. Local development and testing run on a Fedora Linux workstation.
2. Pushing changes to the `main` branch triggers a **GitHub Actions** workflow.
3. The workflow automatically authenticates with AWS and syncs the latest build directly to the S3 bucket.
4. A CloudFront cache invalidation is triggered automatically so new content is served globally within seconds.

## About Me

I am an IT professional with extensive experience in Linux systems, currently working toward becoming a DevOps Engineer. I am actively studying for my AWS Solutions Architect - Associate (SAA-C03) certification to solidify my cloud foundation. My ultimate long-term goal is to work with enterprise open-source solutions, specifically focusing on Red Hat's AI stacks.
