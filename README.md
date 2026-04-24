
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
<img width="1911" height="808" alt="dce2e80ce172860be4b7c20695702f40" src="https://github.com/user-attachments/assets/1c4512f4-810c-4bec-bd4e-2085436bfac7" />
<img width="1892" height="811" alt="de8c9c705c607ef7e36b2ea1783c826f" src="https://github.com/user-attachments/assets/f52fea74-a955-4146-bc08-cac6c6378d09" />


S3 Block Public Access settings  
<img width="1920" height="797" alt="8c2949e3b1a392c6f6a0509ee0117636" src="https://github.com/user-attachments/assets/77ca9365-9576-49cc-a3f7-0741192da7c6" />


AccessDenied (URL)  
<img width="1624" height="628" alt="4ab17a19b2969b9e742dead481a329d1" src="https://github.com/user-attachments/assets/1b3bffd0-7821-4c97-950a-72b663645bbc" />


IAM Role configuration  
<img width="1920" height="802" alt="7361de641d6edba684ef8e4777fdbde7" src="https://github.com/user-attachments/assets/4c98612b-4c6f-49ce-857a-0df93bc1b137" />


EC2 attach role  
<img width="1904" height="536" alt="9961923fbc531b032bf1c0f26bde9ef8" src="https://github.com/user-attachments/assets/ddf72545-8bbf-4dfd-aefb-b4cc90ec4598" />


EC2 download from S3 (CLI)  
<img width="1589" height="561" alt="6df3f7385c6232c26e15f1f8ad893ab6" src="https://github.com/user-attachments/assets/2f3a51e3-9851-44b6-8ee8-a511a31f11ac" />


CloudWatch metrics  
<img width="1920" height="835" alt="423e1323b029d6158c1b5f0929d1485e" src="https://github.com/user-attachments/assets/5f52035c-f674-45af-b7c9-2038589842e5" />


---

Built a secure AWS architecture where a private S3 bucket is accessed by EC2 using IAM Role, verified access control behavior, and monitored system activity via CloudWatch.
```
