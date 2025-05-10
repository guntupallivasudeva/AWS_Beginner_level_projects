# AWS Web Server Hosting Project

This project demonstrates how to host a web server on AWS using the following AWS services:
- **EC2** (Elastic Compute Cloud)
- **S3** (Simple Storage Service)
- **VPC** (Virtual Private Cloud)
- **Key Pair**
- **Security Groups**

---

## 📊 Architecture Diagram

![Screenshot 2025-05-10 170136](https://github.com/user-attachments/assets/44a6b296-3199-4202-8c22-47b0c1108500)

---

## 🚀 Project Overview

The goal is to deploy a basic web application (e.g., an HTML page or a static site) on an EC2 instance, store files/assets in an S3 bucket, and manage secure access using a VPC, key pair, and security groups.

---

## 🧰 Prerequisites

- An active AWS account
- AWS CLI installed and configured
- SSH client (like Terminal, PuTTY, or VS Code Remote SSH)
- IAM permissions to manage EC2, S3, VPC, and security groups

---

## 🔧 Setup Instructions

### 1. Create a Key Pair

```bash
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
chmod 400 MyKeyPair.pem
```

### 2. Create a VPC

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

Save the VPC ID returned from this command.

### 3. Create a Subnet

```bash
aws ec2 create-subnet --vpc-id <your-vpc-id> --cidr-block 10.0.1.0/24
```

### 4. Create an Internet Gateway and Attach to VPC

```bash
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --internet-gateway-id <gateway-id> --vpc-id <your-vpc-id>
```

### 5. Modify Route Table for Internet Access

```bash
aws ec2 describe-route-tables --filters "Name=vpc-id,Values=<your-vpc-id>"
aws ec2 create-route --route-table-id <route-table-id> --destination-cidr-block 0.0.0.0/0 --gateway-id <gateway-id>
```

### 6. Create a Security Group

```bash
aws ec2 create-security-group --group-name WebSG --description "Allow HTTP and SSH" --vpc-id <your-vpc-id>
aws ec2 authorize-security-group-ingress --group-id <group-id> --protocol tcp --port 22 --cidr 0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id <group-id> --protocol tcp --port 80 --cidr 0.0.0.0/0
```

### 7. Launch EC2 Instance

```bash
aws ec2 run-instances \
  --image-id ami-0c02fb55956c7d316 \  # Amazon Linux 2 (Update if needed)
  --instance-type t2.micro \
  --key-name MyKeyPair \
  --security-group-ids <group-id> \
  --subnet-id <subnet-id> \
  --associate-public-ip-address \
  --user-data file://setup.sh
```

> `setup.sh` contains EC2 user-data to install a web server:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello from EC2 Web Server</h1>" > /var/www/html/index.html
```

---

## 🗂️ Set Up S3 Bucket

```bash
aws s3 mb s3://my-web-assets-bucket
aws s3 cp my-image.jpg s3://my-web-assets-bucket/
aws s3api put-bucket-policy --bucket my-web-assets-bucket --policy file://bucket-policy.json
```

> `bucket-policy.json` should look like:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-web-assets-bucket/*"
    }
  ]
}
```

Now you can reference assets like `https://my-web-assets-bucket.s3.amazonaws.com/my-image.jpg` in your web pages.

---

## 🔍 Access Your Web Server

1. Get your EC2 instance’s public IP:

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].PublicIpAddress' --output text
```

2. Visit `http://<your-ec2-ip>` in a browser.

---

## 🧼 Cleanup

To avoid charges, terminate your EC2 instance and delete the created resources:

```bash
aws ec2 terminate-instances --instance-ids <instance-id>
aws ec2 delete-key-pair --key-name MyKeyPair
aws s3 rb s3://my-web-assets-bucket --force
aws ec2 delete-security-group --group-id <group-id>
aws ec2 detach-internet-gateway --internet-gateway-id <gateway-id> --vpc-id <your-vpc-id>
aws ec2 delete-internet-gateway --internet-gateway-id <gateway-id>
aws ec2 delete-subnet --subnet-id <subnet-id>
aws ec2 delete-vpc --vpc-id <your-vpc-id>
```

---

## 📎 Resources

- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- [Amazon EC2 Getting Started Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
- [Amazon S3 Documentation](https://docs.aws.amazon.com/s3/)

---

## 🧠 Author

**Your Name**  
GitHub: [@vasudevaguntupalli](https://github.com/vasudevaguntupalli)
