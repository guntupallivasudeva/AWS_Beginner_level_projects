# 🌐 AWS VPC Setup Guide - MyOrg Configuration  

This guide provides a step-by-step process for creating a VPC Peering Connection between two VPCs in the **Asia Pacific (Hyderabad)** region (`ap-south-2`) using the AWS Console.

## VPC Peering - Connect multiple VPCs together

----
## 🔧 Configuration Details

- **VPC Name**: `MyOrg VPC-1`
- **Public Subnet Name**: `MyOrg VPC-1 Public Subnet`
- **Internet Gateway Name**: `MyOrg VPC-1 IG`
- **Route Tables**: `MyOrg VPC-1 Public Route Table`.
- **Security Groups**: `MyOrg VPC-1 Public SG`.
- **Network ACLs**: `MyOrg VPC-1 Public Network ACL`.
- **EC2 Instances**: `MyOrg VPC-1 Public Server`.

- **VPC Name**: `MyOrg VPC-2`
- **Public Subnet Name**: `MyOrg VPC-2 Public Subnet`
- **Internet Gateway Name**: `MyOrg VPC-2 IG`
- **Route Tables**: `MyOrg VPC-2 Public Route Table`.
- **Security Groups**: `MyOrg VPC-2 Public SG`.
- **Network ACLs**: `MyOrg VPC-2 Public Network ACL`.
- **EC2 Instances**: `MyOrg VPC-2 Public Server`.
- **VPC Peering Connection Name**: `VPC 1 <> VPC 2`
- **VPC Peering Connection Region**: `Asia Pacific (Hyderabad) ap-south-2`
- **VPC Peering Connection Account**
- **VPC Peering Connection VPC ID (Requester)**: `MyOrg VPC-1`
- **VPC Peering Connection VPC ID (Accepter)**: `MyOrg VPC-2`
- **VPC Peering Connection Status**: `Active`
- **VPC Peering Connection Route Table Update**: `Yes, Modify my route tables now`
- **VPC Peering Connection Security Group Update**: `Yes, Modify my security groups now`
- **VPC Peering Connection EC2 Instances**: `Instance MyOrg VPC-1`, `Instance MyOrg VPC-2`
- **VPC Peering Connection Description**: `Peering connection between MyOrg VPC-1 and MyOrg VPC-2`

---

## 📘 Step-by-Step Instructions

(Previous setup steps for VPC, subnets, route tables, NACLs...)

---

## Project Architecture Diagram

![VPC Peering Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Project%20Architecture.png?raw=true)

---

## 📡26. Setup Your VPCs in Minutes using VPCs and More

1. Go to the **VPC Dashboard**.
2. Click on **VPCs** in the left-hand menu.
3. Click on **Create VPC**.
4. Select on VPC & more : 
    - **VPC Name**: `MyOrg VPC-1`
    - **IPv4 CIDR block**: `10.1.0.0/16`
    - **IPv6 CIDR block**: `No IPv6 CIDR block`
    - **Tenancy**: `Default`
    - **Number of Availability Zones (AZs)**: `1`
    - **Number of public subnets**: `1`.
    - **Number of private subnets**: `0`.
    - **NAT gateways**: `None`.
    - **VPC endpoints**: `None`.
    - **DNS options**: `Checked`.
5. Create VPC.

![VPC 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/1.%20VPC-1.png?raw=true)
![VPC 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/2.%20VPC-1.png?raw=true)
![VPC-1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/3.%20VPC-1.png?raw=true)
![Resource Map](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/4.%20VPC-1%20Resource%20Map.png?raw=true)

6. Repeat the above steps to create a second VPC:
    - **VPC Name**: `MyOrg VPC-2`
    - **IPv4 CIDR block**: `10.2.0.0/16`
    - **IPv6 CIDR block**: `No IPv6 CIDR block`
    - **Tenancy**: `Default`
    - **Number of Availability Zones (AZs)**: `1`
    - **Number of public subnets**: `1`.
    - **Number of private subnets**: `0`.
    - **NAT gateways**: `None`.
    - **VPC endpoints**: `None`.
    - **DNS options**: `Checked`.
5. Create VPC.

![VPC 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/5.%20VPC-2.png?raw=true)
![VPC 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/6.%20VPC-2.png?raw=true)
![VPC-1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/7.%20VPC-2.png?raw=true)
![Resource Map](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/8.%20VPC-2%20Resource%20Map%20.png?raw=true)

---

## 🔧 27. Create VPC Peering Connection

1. In the **VPC Dashboard**, click on **Peering Connections** in the left-hand menu.
2. Click on **Create Peering Connection**.
3. Fill in the details:
    - **Peering connection name**: `VPC 1 <> VPC 2`
    - **VPC ID (Requester)**: Select `MyOrg VPC-1`
    - **Account**: `My account`
    - **Region**: `Asia Pacific (Hyderabad) ap-south-2`
    - **VPC ID (Accepter)**: Select `MyOrg VPC-2`
4. Click on **Create Peering Connection**.

![VPC Peering Connection](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/9.%20Create%20Peering.png?raw=true)
![VPC Peering Connection](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/10.%20Create%20Peering.png?raw=true)

5. After creation, The green success bar says the peering connection has been requested.
    - Select the peering connection and click on **Actions** > **Accept Request**.
    - Confirm the acceptance by clicking on **Yes, Accept**.
    - The status will change to **Active**.
    - **Modify my route tables now**

![Accept VPC Peering Connection](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/11.%20VPC%20Peering%20Created%20&%20requested.png?raw=true)
![Accepting action](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/12.%20.png?raw=true)
![Accept Request](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/13.%20Accepting%20the%20request.png?raw=true)

---
## ✍️ 28. Update Route Tables

![Modify Route Tables](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/14.%20Modify%20the%20Routetable.png?raw=true)

1. In the **VPC Dashboard**, click on **Route Tables** in the left-hand menu.
2. Select the route table associated with `MyOrg-1-rtb-public`.
3. Click on the **Routes** tab.
4. Click on **Edit routes**.
5. Click on **Add route**.
6. Fill in the details:
    - **Destination**: `10.2.0.0/16`
    - **Target**: `VPC <> VPC 2`
7. Click on **Save routes**.`

![Adding Route](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/15.%20Adding%20New%20Route%20ofr%20VPC1.png?raw=true)
![Route Table Updated](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/16.%20new%20Route%20added%20vpc1.png?raw=true)

8. Repeat the above steps for the route table associated with `MyOrg-2-rtb-public`:
    - **Destination**: `10.1.0.0/16`
    - **Target**: `VPC <> VPC 1`
9. Click on **Save routes**.

![Adding Route](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/17.%20Adding%20New%20Route%20To%20VPC%202.png?raw=true)
![Route Table Updated](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/18.%20new%20route%20added%20to%20vpc%202.png?raw=true)

---
## 🚀 29. Launch EC2 Instances

1. In the **EC2 Dashboard**, click on **Instances** in the left-hand menu.
2. Click on **Launch instance**.
3. Select the following options:
    - **Name**: `Instance MyOrg VPC-1`
    - **AMI**: `Amazon Linux 2023 AMI`
    - **Instance type**: `t3.micro` Free tier eligible
    - **Key pair (login)**: Proceed without a key pair (not recommended)
    - **VPC**: `MyOrg VPC-1`
    - **Subnet**: `MyOrg VPC-1 Public Subnet`
    - **Auto-assign Public IP**: `Disable`
    - **Security group**: `Default security group`
4. Click on **Launch instance**.
![Instance name](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/19.%20Insatnce%20name.png?raw=true)
![Instance Network](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/19.1.%20%20Instance%201.png?raw=true)
![summary](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/19.1.%20%20Instance%201.png?raw=true)

6. Repeat the above steps to launch another instance in `MyOrg VPC-2`:
    - **Name**: `Instance MyOrg VPC-2`
    - **AMI**: `Amazon Linux 2023 AMI`
    - **Instance type**: `t3.micro` Free tier eligible
    - **Key pair (login)**: Proceed without a key pair (not recommended)
    - **VPC**: `MyOrg VPC-2`
    - **Subnet**: `MyOrg VPC-2 Public Subnet`
    - **Auto-assign Public IP**: `Disable`
    - **Security group**: `Default security group`
7. Click on **Launch instance**.
![Instance summary](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/21.%20Instance%202%20.png?raw=true)
![Instance network](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/22.%20instance%202.png?raw=true)
![Instances Created](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/23.%20Both%20Created%20Instances.png?raw=true)

---
## 🔌 30. Connect to Instance 1

1. In the **EC2 Dashboard**, click on **Instances** in the left-hand menu.
2. Select the instance `Instance MyOrg VPC-1`.
3. Click on **Connect**.
4. we see a error message saying "No public IPv4 address assigned".
5. verify the instance is in a public subnet and has a public IP assigned.
6. If not, go back to the EC2 Dashboard, select **Elastic IPs** in the left-hand menu, and allocate a new Elastic IP.
7. Associate the Elastic IP with `Instance MyOrg VPC-1`.
8. Leave all other settings as default.
9. selecct allocated Elastic IP and click on **Actions** > **Associate Elastic IP address**.
10. Select `Instance MyOrg VPC-1` and click on **Associate**.

![Associate Elastic IP](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/24.%20Elastic%20ip.png?raw=true)

11. Now, go back to the **EC2 Dashboard** and select `Instance MyOrg VPC-1`.
12. Click on **Connect**.
13. Again we see an error message
14. Head back to the **VPC Dashboard** and copy the **VPC ID** of `MyOrg VPC-1`.
15. Head to Security Groups in the left-hand menu.
16. Select the security group associated with `MyOrg VPC-1` Using the **VPC ID** In search bar.
17. select the default security group.
18. Click on the **Inbound rules** tab.
19. Click on **Edit inbound rules**.
20. Click on **Add rule**.
21. Fill in the details:
    - **Type**: `SSH`
    - **Protocol**: `TCP`
    - **Port range**: `22`
    - **Source**: `Anywhere-IPv4`
22. Click on **Save rules**.
23. now go back to the **EC2 Dashboard** and select `Instance MyOrg VPC-1`.
24. Click on **Connect**.
25. Success! You are now connected to `Instance MyOrg VPC-1`.

![Connect to Instance MyOrg VPC-1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/25.%20Adding%20inbound%20rules%20to%20Sg.png?raw=true)
![Connect to Instance MyOrg VPC-1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/26.%20edit%20inbound%20of%20sg%20of%20insatance%201.png?raw=true)

---

## 31. Test VPC Peering Connection

1. In the **EC2 Dashboard**, click on **Instances** in the left-hand menu.
2. Select the instance `Instance MyOrg VPC-2`.
3. Copy Private IPv4 address of `Instance MyOrg VPC-2`.

![Copy Private IPv4 address](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/27.%20Test%20Peer%20Connectivity%20Using%20VPC2%20Private%20address.png?raw=true)

4. Switch back to the terminal of `Instance MyOrg VPC-1`.
5. Run the command `ping [Private IPv4 address of Instance MyOrg VPC-2]`.
    - `ping 10.2.6.38` in my case.
6. so we have a small error 
7. so head to check whether inbound rules of `MyOrg VPC-2` security group is allowing ICMP traffic.
8. Copy the **VPC ID** of `MyOrg VPC-2`.
9. Head to Security Groups in the left-hand menu.
10. Select the security group associated with `MyOrg VPC-2` using the **VPC ID** in the search bar.
11. Select the default security group.
12. Click on the **Inbound rules** tab. 
13. Click on **Edit inbound rules**.
14. Click on **Add rule**.
15. Fill in the details:
    - **Type**: `All ICMP - IPv4`
    - **Protocol**: `ICMP`
    - **Port range**: `N/A`
    - **Source**: `10.1.0.0/16`
16. Click on **Save rules**.
17. Now go back to the terminal of `Instance MyOrg VPC-1`.
18. You should see a response indicating successful connectivity between the two VPCs.

![Final VPC Peering Connection](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/6.%20VPC%20Peering%20Connection/Images/28.%20Final%20Connectivity.png?raw=true)

---

## ✅ Final Updated Summary

----------------------------------------------------------
| Component        | Name                                |
|------------------|-------------------------------------|
| VPC              | `MyOrg VPC-1`                       |
|                  | `MyOrg VPC-2`                       |
| Subnet           | `MyOrg VPC-1 Public Subnet`         |
|                  | `MyOrg VPC-2 Public Subnet`         |
| Internet Gateway | `MyOrg VPC-1 IG`                    |
|                  | `MyOrg VPC-2 IG`                    |
| Route Tables     | `MyOrg VPC-1 Public Routetable`    |
|                  | `MyOrg VPC-2 Public Routetable`    |
| Security Groups  | `MyOrg VPC-1 Public SG`,            |
|                  | `MyOrg VPC-2 Public SG`             |
| Network ACLs     | `MyOrg VPC-1 Public Network ACL`    |
|                  | `MyOrg VPC-2 Public Network ACL`    |
| EC2 Instances    | `Instance - MyOrg VPC-1`            |
|                  | `Instance - MyOrg VPC-2`            |
----------------------------------------------------------

---
## 📂 Final Project Structure Overview

```text
AWS Cloud Account:
├── VPC
│   └── MyOrg VPC-1
│   └── MyOrg VPC-2
├── Subnets
│   ├── MyOrg VPC-1 Public Subnet
│   └── MyOrg VPC-2 Public Subnet
├── Internet Gateway
│   └── MyOrg VPC-1 IG
│   └── MyOrg VPC-2 IG
├── Route Tables
│   ├── MyOrg VPC-1 Public Routetable
│   └── MyOrg VPC-2 Public Routetable
├── Security Groups
│   ├── MyOrg VPC-1 Public SG
│   └── MyOrg VPC-2 Public SG
├── Network ACLs
│   ├── MyOrg VPC-1 Public Network ACL
│   └── MyOrg VPC-2 Public Network ACL
├── EC2 Instances
│   ├── Instance - MyOrg VPC-1
│   └── Instance - MyOrg VPC-2
│
```

---

#### ✍️ Author  

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

----
