
# 🌐 AWS VPC Setup Guide - MyOrg Configuration  

This guide provides a step-by-step process for creating a Virtual Private Cloud (VPC), a subnet,an internet gateway, and Route Table in the **Asia Pacific (Hyderabad)** region (`ap-south-2`) using AWS Console.  

## 🔧 Configuration Details  

- **VPC Name**: `MyOrg VPC`  
- **VPC CIDR**: `10.0.0.0/16`  
- **Subnet Name**: `MyOrg Subnet`  
- **Subnet CIDR**: `10.0.1.0/24`  
- **Availability Zone**: `ap-south-2a`  
- **Internet Gateway Name**: `MyOrg IG`  

---

## 📘 Step-by-Step Instructions  

### 1. Create the VPC  

1. Navigate to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).  
2. Click **Create VPC**.  
3. Select **VPC and more**.  
4. Under **Name tag**, enter `MyOrg VPC`.  
5. For **IPv4 CIDR block**, enter `10.0.0.0/16`.  
6. Leave other settings as default.  
7. Click **Create VPC**.  

---

### 2. Create a Subnet  

1. Go to **Subnets** in the VPC Dashboard.  
2. Click **Create subnet**.  
3. Select `MyOrg VPC` from the dropdown.  
4. Enter `MyOrg Subnet` as the subnet name.  
5. Choose **Availability Zone**: `ap-south-2a`.  
6. Enter CIDR block `10.0.1.0/24`.  
7. Click **Create subnet**.  

---

### 3. Create an Internet Gateway  

1. Go to **Internet Gateways** in the VPC Dashboard.  
2. Click **Create internet gateway**.  
3. Enter the name `MyOrg IG`.  
4. Click **Create internet gateway**.  
5. Select it, then go to **Actions** > **Attach to VPC**.  
6. Choose `MyOrg VPC` and click **Attach**.  

---

### 4. Update the Route Table  

1. Go to **Route Tables**.  
2. Locate the route table associated with `MyOrg VPC`.  
3. Click on it and open the **Routes** tab.  
4. Click **Edit routes** > **Add route**.  
5. Destination: `0.0.0.0/0`  
6. Target: Select `Internet Gateway`, then choose `MyOrg IG`.  
7. Click **Save routes**.  

---

### 5. Associate the Subnet with Route Table  

1. Open the same Route Table and go to **Subnet associations** tab.  
2. Click **Edit subnet associations**.  
3. Select `MyOrg Subnet` and click **Save associations**.  

---

### 6. Enable Auto-Assign Public IP  

1. Go to **Subnets**.  
2. Select `MyOrg Subnet`.  
3. Click **Actions** > **Modify auto-assign IP settings**.  
4. Enable **Auto-assign public IPv4 address**.  
5. Click **Save**.  

---

## ✅ Summary  

- **VPC**: `MyOrg VPC` (CIDR: `10.0.0.0/16`)  
- **Subnet**: `MyOrg Subnet` in `ap-south-2a` (CIDR: `10.0.1.0/24`)  
- **Internet Gateway**: `MyOrg IG` attached to VPC  
- **Route Table**: Routes `0.0.0.0/0` via `MyOrg IG`  
- **Public IP**: Auto-assigned for subnet  

---
## 📂 Project Structure Overview  

```text
AWS Cloud Account:
├── VPC 
│   └── MyOrg VPC  
├── Subnets
│   └── MyOrg Subnet 
├── Internet Gateway
│   └── MyOrg IG
├── Route Tables
│   └── MyOrg Route Table

```

---

## 🏗️ Project Architecture  

| Component        | Name               |
|------------------|--------------------|
| VPC              | `MyOrg VPC`        |
| Subnet           | `MyOrg Subnet`     |
| Internet Gateway | `MyOrg IG`         |
-----------------------------------------

## Architecture Diagram  

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/1.%20Build%20A%20Virtual%20Private%20Cloud%20With%20Subnets,%20Internet-Gateway,%20Routetable/Images/Project%20Architecture.png?raw=true)
  
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
