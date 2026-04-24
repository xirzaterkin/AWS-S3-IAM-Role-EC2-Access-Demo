
---

```markdown
# AWS S3 + IAM Role + EC2 Access Demo

📌 Overview  
This project demonstrates secure access to a private S3 bucket from an EC2 instance using IAM Role (without using access keys).

IAM User / Group (S3権限)  
S3 Bucket（非公開設定）  
IAM Role（EC2用）  
EC2（S3アクセス）  
CloudWatch（監視）  

The goal is to understand the difference between public access and IAM-based access, and how EC2 securely interacts with S3.

---

🧾 概要  
本プロジェクトでは、IAMロールを利用してEC2からS3へ安全にアクセスする構成を構築した。  

IAMユーザー・ユーザーグループの作成  
S3バケットの非公開設定（Block Public Access）  
IAMロールの作成およびEC2への付与  
EC2からS3へのアクセス検証  
CloudWatchによる監視  

S3の公開アクセスとIAM認証の違い、および安全なアクセス方法を理解することを目的とする。  

---

🏗 Architecture  

EC2 Instance  
  ↓ (IAM Role)  
S3 Bucket (Private)  

---

⚙️ Implementation Steps  

Create IAM user and user group (S3 permissions)  
Create S3 bucket and enable Block Public Access  
Upload test file to S3  
Access object via URL → AccessDenied  
Create IAM Role for EC2  
Attach AmazonS3FullAccess policy  
Attach IAM Role to EC2 instance  
Access S3 using AWS CLI from EC2  
Download object from S3  
Monitor EC2 using CloudWatch  

---

🧪 Verification  

Verify IAM Role:  

```

aws sts get-caller-identity

```

Download file:  

```

aws s3 cp s3://your-bucket/file.png .

```

Check file:  

```

ls

```

---

📊 Observations  

S3 public URL access was denied  
EC2 successfully accessed S3 using IAM Role  
File download confirmed  
CloudWatch showed network activity during download  

---

⚠️ Troubleshooting  

AccessDenied when using URL  
S3 access initially failed from EC2  

Analysis:  

S3 Block Public Access prevents direct URL access  
IAM Role was not attached or permissions not applied  

Solution:  

Attach IAM Role to EC2  
Ensure correct S3 permissions (FullAccess or ReadOnly)  
Retry using AWS CLI  

---

📚 Learnings  

Understood difference between public access and IAM access  
Learned how IAM Role works with EC2  
Verified secure access without access keys  
Practiced AWS CLI operations  
Observed resource behavior via CloudWatch  

---

💡 Key Takeaway  

Secure AWS access should use IAM Role instead of access keys  

S3 public access must be explicitly allowed  
EC2 can securely access S3 via IAM Role  
CloudWatch helps verify system behavior  

---

🚀 Future Improvements  

Use IAM policy least privilege instead of FullAccess  
Add VPC Endpoint for S3 (no internet needed)  
Integrate CloudFront for CDN  
Add logging and monitoring enhancements  

---

📸 Screenshots  

IAM user and group  
image  

S3 Block Public Access settings  
image  

AccessDenied (URL)  
image  

IAM Role configuration  
image  

EC2 attach role  
image  

EC2 download from S3 (CLI)  
image  

CloudWatch metrics  
image  

---

Built a secure AWS architecture where a private S3 bucket is accessed by EC2 using IAM Role, verified access control behavior, and monitored system activity via CloudWatch.
```
