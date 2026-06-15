# S3 Static Website Hosting Architecture (Mermaid)

```mermaid
flowchart LR
    User["👤 User / Browser"] -->|DNS lookup| R53["Amazon Route 53<br/>(DNS)"]
    R53 -->|Routes to| CF["Amazon CloudFront<br/>(CDN)"]
    CF -->|Origin fetch| S3["Amazon S3 Bucket<br/>(Static Website Hosting)<br/>HTML / CSS / JS / Images"]
    ACM["AWS Certificate Manager<br/>(SSL/TLS)"] -.->|HTTPS cert| CF

    style User fill:#fff,stroke:#232F3E,stroke-width:2px
    style R53 fill:#e6d6ff,stroke:#8C4FFF,stroke-width:2px
    style CF fill:#e6d6ff,stroke:#8C4FFF,stroke-width:2px
    style ACM fill:#fff,stroke:#232F3E,stroke-width:2px
    style S3 fill:#e6f0d6,stroke:#7AA116,stroke-width:2px
```

## Components

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
