# 🌐 AWS VPC Setup Guide - MyOrg Configuration

This guide provides a step-by-step process for creating a Virtual Private Cloud (VPC), a subnet, an internet gateway, and related networking components in the **Asia Pacific (Hyderabad)** region (`ap-south-2`) using AWS Console.

## 🔧 Configuration Details

- **VPC Name**: `MyOrg VPC`
- **VPC CIDR**: `10.0.0.0/16`
- **Subnet Name**: `MyOrg Subnet`
- **Subnet CIDR**: `10.0.1.0/24`
- **Availability Zone**: `ap-south-2a`
- **Internet Gateway Name**: `MyOrg IG`

---

## 📘 Step-by-Step Instructions

## 🏗️ Project Architecture

| Component        | Name               |
|------------------|--------------------|
| VPC              | `MyOrg VPC`        |
| Subnet           | `MyOrg Subnet`     |
| Internet Gateway | `MyOrg IG`         |
| Route Table      | `MyOrg Route Table`|
| Security Group   | `MyOrg SG`         |
| Network ACL      | `MyOrg Network ACL`|
-----------------------------------------
---

### Project Architecture Diagram

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/2.%20VPC%20Traffic%20Flow%20and%20Security/Project%20Architeture.png?raw=true)


### 1. Create the VPC

1. Navigate to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).
2. Click **Create VPC**.
3. Select **VPC and more**.
4. Under **Name tag**, enter `MyOrg VPC`.
5. For **IPv4 CIDR block**, enter `10.0.0.0/16`.
6. Leave other settings as default.
7. Click **Create VPC`.

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

### 7. Create a Route Table

1. Go to **Route Tables** in the VPC Dashboard.
2. Click **Create route table**.
3. Enter `MyOrg Route Table` as the name.
4. Select `MyOrg VPC` from the dropdown.
5. Click **Create route table**.

---

### 8. Add Route to Internet Gateway

1. Select `MyOrg Route Table`.
2. Go to the **Routes** tab and click **Edit routes**.
3. Click **Add route**.
4. Set **Destination** to `0.0.0.0/0`.
5. Set **Target** to the Internet Gateway: `MyOrg IG`.
6. Click **Save routes**.

---

### 9. Associate Route Table with Subnet

1. With `MyOrg Route Table` selected, go to the **Subnet associations** tab.
2. Click **Edit subnet associations**.
3. Select `MyOrg Subnet`.
4. Click **Save associations**.

---

### 10. Create a Security Group

1. Go to **Security Groups** in the VPC Dashboard.
2. Click **Create security group**.
3. Name it `MyOrg SG`.
4. Select `MyOrg VPC`.
5. Add an **Inbound rule**:
   - Type: `HTTP`
   - Protocol: `TCP`
   - Source: `0.0.0.0/0`
6. Click **Create security group**.

---

### 11. Create a Network ACL

1. Go to **Network ACLs** under VPC Dashboard.
2. Click **Create Network ACL**.
3. Name it `MyOrg Network ACL`.
4. Select `MyOrg VPC`.
5. Click **Create**.

---

### 12. Add Inbound and Outbound Rules (Rule #100)

#### Inbound Rule:
- Rule Number: `100`
- Type: `All Traffic`
- Protocol: `All`
- Source: `0.0.0.0/0`
- Allow/Deny: `ALLOW`

#### Outbound Rule:
- Rule Number: `100`
- Type: `All Traffic`
- Protocol: `All`
- Destination: `0.0.0.0/0`
- Allow/Deny: `ALLOW`

---

### 13. Associate Network ACL with Subnet

1. Open the newly created `MyOrg Network ACL`.
2. Go to the **Subnet associations** tab.
3. Click **Edit subnet associations**.
4. Select `MyOrg Subnet`.
5. Click **Save`.

---
### ✅ Verification  

- Check the Resource Map by selecting the VPC in the VPC Dashboard Check the mapping.  
- Ensure all components are correctly associated.  
- Check the **Route Table** to confirm the route to `0.0.0.0/0` via `MyOrg IG`.  
- Verify the **Security Group** rules to ensure HTTP access is allowed.  
- Check the **Network ACL** rules to confirm all traffic is allowed.  
- Ensure the **Subnet** has auto-assign public IP enabled.  
- Verify the **Internet Gateway** is attached to the VPC.  

---

## ✅ Updated Summary

- **VPC**: `MyOrg VPC` (CIDR: `10.0.0.0/16`)  
- **Subnet**: `MyOrg Subnet` in `ap-south-2a` (CIDR: `10.0.1.0/24`)  
- **Internet Gateway**: `MyOrg IG` attached to VPC  
- **Route Table**: `MyOrg Route Table`, routes `0.0.0.0/0` via `MyOrg IG`, associated with subnet `MyOrg Subnet`
- **Public IP**: Auto-assigned for subnet `MyOrg Subnet`
- **Security Group**: `MyOrg SG` with HTTP inbound rule  
- **Network ACL**: `MyOrg Network ACL`, all traffic allowed (rule 100), associated with subnet  `MyOrg Subnet`  

---

## 📂 Updated Project Structure Overview

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
├── Security Groups
│   └── MyOrg SG
├── Network ACLs
│   └── MyOrg Network ACL
```

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
