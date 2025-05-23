# 🌐 AWS VPC Setup Guide - MyOrg Configuration

This guide provides a step-by-step process for creating a Public and Private Subnet architecture within a Virtual Private Cloud (VPC) in the **Asia Pacific (Hyderabad)** region (`ap-south-2`) using the AWS Console.

## 🔧 Configuration Details

- **VPC Name**: `MyOrg VPC`
- **Public Subnet Name**: `MyOrg Public Subnet`
- **Private Subnet Name**: `MyOrg Private Subnet`
- **Internet Gateway Name**: `MyOrg IG`
- **Route Tables**: `MyOrg Public Route Table`, `MyOrg Private Route Table`
- **Security Groups**: `MyOrg Public SG`, `MyOrg Private SG`
- **Network ACLs**: `MyOrg Public Network ACL`, `MyOrg Private Network ACL`
- **Key Pair**: `MyOrg KeyPair (.pem)`
- **EC2 Instances**: `MyOrg Public Server`, `MyOrg Private Server`

---

## 📘 Step-by-Step Instructions

(Previous setup steps for VPC, subnets, route tables, NACLs...)

---

### 19. Launch a Public EC2 Instance

1. Go to **Instances** > **Launch Instance**.
2. Name: `MyOrg Public Server`
3. OS: **Amazon Linux 2023 AMI**
4. Type: `t3.micro`
5. Key pair: Click on **Create key pair**.
   - Name it: `MyOrg KeyPair`
   - Format: `.pem`
   - Click **Create key pair** and download the file securely.
6. Network: `MyOrg VPC`, Subnet: `MyOrg Public Subnet`
7. Enable auto-assign public IP
8. Select Existing security group: `MyOrg Public SG`,
9. Click **Launch Instance**

---

### 20. Launch a Private EC2 Instance

1. Select **Launch Instance** again.
2. Name: `MyOrg Private Server`
3. OS: **Amazon Linux 2023 AMI**
4. Type: `t3.micro`
5. Key pair: `MyOrg KeyPair`
6. Network: select Edit at the right hand corner.
   - `MyOrg VPC`, Subnet: `MyOrg Private Subnet`   
7. Auto-assign public IP: **Disabled**
8. Select security group: Select **Create Security Group**
   - Name: `MyOrg Private SG`
   - Description: `Security group for MyOrg Private Subnet.
   - VPC: `MyOrg VPC`
   - Inbound Rule:
     - Type: **ssh**
     - Protocol: **TCP**
     - Port Range: **22**
     - Source Type: `Custom`
     - Source: `MyOrg Public SG`
     - Description: `Allow SSH from MyOrg Public SG`
9. Click **Launch Instance**

---

### 21. Verify VPC 

1. Go to **VPC Dashboard**.
2. Select **create VPC**.
3. Select **VPC and more**.
4. Now check the **Resource Map**.
5. Change the name of prefix to `MyOrg`.
6. It shows the VPC and all the resources with MyOrg Prefix.
7. Verify everything is in place.
8. We can Create all the resources here it self in a single click.  

---

### Verification

- Check the Resource Map by selecting the VPC in the VPC Dashboard Check the mapping.  
- Ensure all components are correctly associated.  
- Check the **Route Table** to confirm the route to `0.0.0.0/0` via `MyOrg IG`.  
- Verify the **Security Group** rules to ensure HTTP access is allowed.  
- Check the **Network ACL** rules to confirm all traffic is allowed.  
- Ensure the **Subnet** has auto-assign public IP enabled.  
- Verify the **Internet Gateway** is attached to the VPC. 
- Ensure the **EC2 Instances** are running and accessible.

---

## ✅ Final Updated Summary

----------------------------------------------------------
| Component         | Name                               |
|------------------|-------------------------------------|
| VPC              | `MyOrg VPC`                         |
| Subnet           | `MyOrg Public Subnet`               |
|                  | `MyOrg Private Subnet`              |
| Internet Gateway | `MyOrg IG`                          |
| Route Tables     | `MyOrg Public Route Table`          |
|                  | `MyOrg Private Route Table`         |
| Security Groups  | `MyOrg Public SG`,                  |
|                  | `MyOrg Private SG`                  |
| Network ACLs     | `MyOrg Public Network ACL`          |
|                  | `MyOrg Private Network ACL`         |
| EC2 Instances    | `MyOrg Public Server`               |
|                  | `MyOrg Private Server`              |
| Key Pair         | `MyOrg KeyPair (.pem)`              |
----------------------------------------------------------

---

## 📂 Final Project Structure Overview

```text
AWS Cloud Account:
├── VPC 
│   └── MyOrg VPC  
├── Subnets
│   ├── MyOrg Public Subnet 
│   └── MyOrg Private Subnet 
├── Internet Gateway
│   └── MyOrg IG
├── Route Tables
│   ├── MyOrg Public Route Table
│   └── MyOrg Private Route Table
├── Security Groups
│   ├── MyOrg Public SG
│   └── MyOrg Private SG
├── Network ACLs
│   ├── MyOrg Public Network ACL
│   └── MyOrg Private Network ACL
├── EC2 Instances
│   ├── MyOrg Public Server
│   └── MyOrg Private Server
├── Key Pair
│   └── MyOrg KeyPair (.pem)
```

---

### Project Architecture Diagram

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/4.%20Provisioning%20Public%20&%20Private%20Server%20(%20EC2%20)%20to%20our%20Network/Project%20Architecture.png?raw=true)

---

## ✍️ Author

**Vasudeva Guntupalli**  
Cloud & Full Stack Developer  
_This project is part of AWS Security Practices for Beginners._

- [LinkedIn](https://www.linkedin.com/in/guntupallivasudeva/)  
- [GitHub](https://github.com/guntupallivasudeva)

---

## 📌 License

This project is for educational/demo purposes only.  
Feel free to use it for learning and experimentation.  
Happy Cloud Building! ☁️🚀
