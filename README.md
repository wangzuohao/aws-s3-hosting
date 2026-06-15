# aws-s3-hosting

AWS S3 static website hosting architecture diagram (draw.io).

## Architecture Overview

This repository documents a reference architecture for hosting a static website on Amazon S3, fronted by CloudFront for global CDN delivery and HTTPS.

| Component | Role |
|-----------|------|
| **User / Browser** | End user accessing the website over HTTPS |
| **Amazon Route 53** | DNS resolution; maps the custom domain to CloudFront |
| **Amazon CloudFront** | Global CDN that caches and accelerates content delivery; terminates HTTPS |
| **AWS Certificate Manager (ACM)** | Provisions and manages the SSL/TLS certificate for CloudFront |
| **Amazon S3 Bucket** | Origin storing static assets (HTML / CSS / JS / images) |

## Request Flow

1. **DNS lookup** — The user enters the domain; Route 53 resolves it.
2. **Routes to CDN** — The request is routed to the nearest CloudFront edge location.
3. **Origin fetch** — On a cache miss, CloudFront fetches the static files from the S3 bucket.
4. **HTTPS** — The ACM certificate is attached to CloudFront, securing the connection.

## Design Notes

- Enable **Static Website Hosting** on the S3 bucket, or serve it as a private origin behind CloudFront using **OAC/OAID** to restrict direct access.
- Use **CloudFront** for caching, compression, HTTPS, and low-latency global delivery.
- In **Route 53**, use an Alias record pointing to the CloudFront distribution domain.

## Diagram

The editable diagram is located at [`architecture/s3-web-hosting.drawio`](architecture/s3-web-hosting.drawio). Open it with [draw.io](https://app.diagrams.net/).
