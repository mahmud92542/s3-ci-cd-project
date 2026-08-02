# Gourmet Bites - Static Restaurant Website

A professional, high-end restaurant landing page built with a single-file architecture for simple hosting and automated deployment.

## 🚀 Features

* **Modern UI:** Responsive design with smooth animations and hover effects.
* **Dynamic Imagery:** High-quality food photography powered by Unsplash.
* **Automated CI/CD:** Seamless deployment to AWS S3 using GitHub Actions.
* **Lightweight:** Single-file architecture (`index.html`) for lightning-fast load times.

## 🛠 Tech Stack

* **Frontend:** HTML5, CSS3, JavaScript.
* **Hosting:** AWS S3 (Static Website Hosting).
* **CI/CD:** GitHub Actions.

## 🚀 Deployment Instructions

This project uses GitHub Actions to sync files to S3 automatically. Every time you push changes to `index.html` on the `main` branch, the site updates automatically.

### Required GitHub Secrets

To enable deployment, ensure the following **GitHub Secrets** are added to your repository (`Settings > Secrets and variables > Actions`):

* `AWS_S3_BUCKET`: The name of your S3 bucket.
* `AWS_ACCESS_KEY_ID`: Your AWS IAM user access key.
* `AWS_SECRET_ACCESS_KEY`: Your AWS IAM user secret key.

### S3 Bucket Policy

To allow public access to the static website files stored in the S3 bucket, add the following bucket policy. Replace `<S3_ARN>` with the ARN of your S3 bucket:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "<S3_ARN>/*"
        }
    ]
}
```

> **Note:** Make sure your S3 bucket's **Block Public Access** settings allow public access before applying this policy. For production deployments, consider using **CloudFront with Origin Access Control (OAC)** instead of making the S3 bucket publicly accessible.

## 🖥️ EC2 Apache Web Server Setup

To install and configure the Apache HTTP Server (`httpd`) on an Amazon Linux 2 EC2 instance, run the following commands:

```bash
#!/bin/bash

# Update installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Start Apache HTTP Server
systemctl start httpd

# Enable Apache HTTP Server to start automatically after reboot
systemctl enable httpd

# Create a test HTML page
echo "<h1>Hello NSU! $(hostname -f)</h1>" > /var/www/html/index.html
```

This script will:

1. Update the installed packages on the EC2 instance.
2. Install the Apache HTTP Server (`httpd`).
3. Start the Apache web server.
4. Configure Apache to start automatically when the instance reboots.
5. Create a simple HTML page displaying **Hello NSU!** along with the instance's fully qualified hostname.

> **Note:** Ensure that the EC2 instance's **Security Group** allows inbound HTTP traffic on **port 80** so the web server can be accessed from a browser.

## 📂 Project Structure

```text
.
├── .github/
│   └── workflows/
│       └── deploy.yml   # CI/CD pipeline configuration
└── index.html           # Main website code
```
