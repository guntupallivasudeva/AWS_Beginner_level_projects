# 🌐 AWS VPC Setup Guide - MyOrg Configuration

This guide provides a step-by-step process for creating a Public and Private Subnet architecture within a Virtual Private Cloud (VPC) in the **Asia Pacific (Hyderabad)** region (`ap-south-2`) using the AWS Console.

---

## AWS VPC Setup Guide  

### Project Architecture Diagram

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/3.%20Creating%20a%20Private%20Subnet%20,%20Route%20Table,%20Nework%20ACL/Project%20Architecture.png?raw=true)

---


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
4. Enter `MyOrg Public Subnet` as the subnet name.
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

### 4. Update the Route Table (If Route Table create before IG )

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
3. Select `MyOrg Public Subnet` and click **Save associations**.

---

### 6. Enable Auto-Assign Public IP

1. Go to **Subnets**.
2. Select `MyOrg Public Subnet`.
3. Click **Actions** > **Modify auto-assign IP settings**.
4. Enable **Auto-assign public IPv4 address**.
5. Click **Save**.

---

### 7. Create a Route Table

1. Go to **Route Tables** in the VPC Dashboard.
2. Click **Create route table**.
3. Enter `MyOrg Public Route Table` as the name.
4. Select `MyOrg VPC` from the dropdown.
5. Click **Create route table**.

---

### 8. Add Route to Internet Gateway

1. Select `MyOrg Public Route Table`.
2. Go to the **Routes** tab and click **Edit routes**.
3. Click **Add route**.
4. Set **Destination** to `0.0.0.0/0`.
5. Set **Target** to the Internet Gateway: `MyOrg IG`.
6. Click **Save routes**.

---

### 9. Associate Route Table with Subnet

1. With `MyOrg Public Route Table` selected, go to the **Subnet associations** tab.
2. Click **Edit subnet associations**.
3. Select `MyOrg Public Subnet`.
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
3. Name it `MyOrg Public Network ACL`.
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

1. Open the newly created `MyOrg Public Network ACL`.
2. Go to the **Subnet associations** tab.
3. Click **Edit subnet associations**.
4. Select `MyOrg Public Subnet`.
5. Click **Save**.

---
### 14. Create a Private Subnet

1. Go to **Subnets** in the VPC Dashboard.
2. Click **Create subnet**.
3. Select `MyOrg VPC`.
4. Enter `MyOrg Private Subnet` as the subnet name.
5. Choose **Availability Zone**: `ap-south-2b`.
6. Enter CIDR block: `10.0.1.0/24`.
7. Click **Create subnet**.

---

### 15. Create a Private Route Table

1. Go to **Route Tables** in the VPC Dashboard.
2. Click **Create route table**.
3. Name it `MyOrg Private Route Table`.
4. Select `MyOrg VPC`.
5. Click **Create route table**.

---

### 16. Associate Private Subnet with Private Route Table

1. Open `MyOrg Private Route Table`.
2. Go to **Subnet associations** tab.
3. Click **Edit subnet associations**.
4. Select `MyOrg Private Subnet`.
5. Click **Save associations**.

---

### 17. Create a Private Network ACL

1. Go to **Network ACLs**.
2. Click **Create network ACL**.
3. Name it `MyOrg Private Network ACL`.
4. Select `MyOrg VPC`.
5. Click **Create**.

---

### 18. Associate Private Network ACL with Private Subnet

1. Open `MyOrg Private Network ACL`.
2. Go to the **Subnet associations** tab.
3. Click **Edit subnet associations**.
4. Select `MyOrg Private Subnet`.
5. Click **Save**.

---
## 🧠 AWS EC2 Instance Setup Guide

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

### Project Architecture Diagram

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/4.%20Provisioning%20Public%20&%20Private%20Server%20(%20EC2%20)%20to%20our%20Network/Project%20Architecture.png?raw=true)

---
##  📡Testing VPC Connectivity - Verify network communication works Guide  
  
### 22. Connect to MyOrg Public Server  

- Open your EC2 console, select Instances from the left hand navigation panel.  
- Select the checkbox next to `MyOrg Public Server`.  
- Select Connect.  
- Keep all of the default settings.  

![Use Ec2 Instance Connect](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/1.%20EC2%20Instance%20Connet.png?raw=true)  

- Select Connect. 
- We've failed to connect to our instance !.  
- Head back to your VPC console.  
- Head into the Security groups page from the left hand navigation bar.   
- Select the checkbox next to `MyOrg Public Security Group`.  
- Select the Inbound rules tab.  

---

#### 23. Edit Inbound rules in MyOrg Public SG :    

- In the Inbound rules tab, select Edit inbound rules.  
- Select Add rule.  
- For your new rule, configure the Type as `SSH`.  
- Then, under Source type, select Anywhere-IPv4.  
- Select Save rules.  
- With that modified, refresh your EC2 console's Instances page.  
- Select your Public Server and select Connect again.  
- Success.  

![Inbound for Public SG](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/2.%20Allow%20inbound%20trafic%20for%20public%20Security%20group%20from%20SSH.png?raw=true)  

---

- Connection between Public and Private Instances.    
- Leave open the EC2 Instance Connect tab, but head back to your EC2 console in a new tab.  
- Select `MyOrg Private Server`.  
- Copy your private server's Private IPv4 address.  
- Switch back to the EC2 Instance Connect tab.  
- Run ping `[the Private IPv4 address you just copied]` in terminal.  
- Your final result should look similar to something like `ping 10.0.1.223`.

---

![Connected to Public Insatnce](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/3.%20Connected%20to%20Public%20Instance.png?raw=true)

### 24. Test Connectivity Between EC2 Instances :  

- To resolve this connectivity error, let's check whether `MyOrg Private Server` is allowing in ICMP traffic.  
- Leave open the EC2 Instance Connect tab, but head back to your VPC console in a new tab.  
- In the VPC console, select the Subnets page.   
- Select `MyOrg Private Subnet`.   
- Clicking on the link to your `MyOrg Private NACL`.    
- Select the checkbox next to `MyOrg Private NACL`.  
- Select the Inbound rules tab.  
- Select Edit inbound rules.  
- Let's add a new rule to let `MyOrg Public Server` ping `MyOrg Private Server`.  
- Select Add new rule.  
- Assign `100` as the rule number.  
- Change the Type to `All ICMP - IPv4`.  
- Set the Source to traffic coming from your public subnet `10.0.0.0/24`  
- Select Save changes.  

![Edit Inbound add ICMP to NACL](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/4.%20Edit%20inbound%20rule%20add%20ICMP%20traffic%20in%20Private%20NACL.png?raw=true) 

- Let's apply the same to Outbound rules.  
  - Rule number: `100`  
  - Type: `All ICMP - IPv4`.  
  - Source: `10.0.0.0/24`.

![Edit Outbound add ICMP to NACL](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/5.%20Edit%20outbound%20rule%20add%20ICMP%20traffic%20in%20Private%20NACL.png?raw=true)  

- check the security groups! Select Security groups from the left hand navigation panel.  
- Select `MyOrg Private Security Group`.  
- Check your Inbound rules tab - does this security group allow ICMP traffic.  
- Select Edit inbound rules.  
- Select Add rule.  
- For Type, select All ICMP - IPv4.  
- For Source, select `MyOrg Public Security Group`.  
- Select Save rules.  

![Edit Inbound Add ICMP to Private SG](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/6.%20Edit%20inbound%20rule%20add%20ICMP%20traffic%20in%20Private%20SG.png.png?raw=true)  


- Revisit the EC2 Instance Connect tab that's connected to `MyOrg Public Server`.  

![Connectivity Between EC2 Instances](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/7.%20Connectivity%20Between%20EC2%20Insatnces.png?raw=true)

---

### 25. Test the Connectivity with Internet  

- Quit the ping command by pressing Control + C on your keyboard.  
- Let's enter a new command!  
- Type in curl example.com in the prompt, i.e. right after the $ sign at the bottom line of the black window.  
- You should see a response similar to this!  

![Internet Connectivity](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/8.%20%20Final%20internet%20Connectivity.png?raw=true)

**Thats It we Done with Connectivity Check**  

---

### Project Architecture Diagram  

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/4.%20Provisioning%20Public%20&%20Private%20Server%20(%20EC2%20)%20to%20our%20Network/Project%20Architecture.png?raw=true)  

---
## 🌐 AWS VPC Peering Connection Guide 

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

## 🚀 AWS VPC Monitoring with Flow Logs Guide

## Project Architecture Diagram

![VPC Peering Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Project%20Architecture.png?raw=true)

---

### 32. Terminate Previous Instances and  Create New Instances
1. **Terminate Previous Instances**:  
   - Go to the EC2 Dashboard.
   - Select the instances you want to terminate.
   - Click on "Actions" > "Instance State" > "Terminate".
2. **Create New Instances**:
    - Go to the EC2 Dashboard.
    - Click on "Launch Instance".
    - Instance Name: `Instance - MyOrg VPC 1` and  `Instance - MyOrg VPC 2`.
    - Select the AMI as `Amazon Linux 2023 AMI`, instance type as `t3.micro`, and Key Pair select Proceed without a key pair(not recommended).
    - Configure the instance details:
        - Network: Select `MyOrg VPC-1` for the first instance and `MyOrg VPC-2` for the second instance.
        - Subnet: Select the respective public subnet for each VPC.
        - Auto-assign Public IP: Enable this option.
    - Create security group name as `MyOrg SG 1` & `MyOrg SG 2`.
        - Allow inbound traffic on port 22 (SSH) from your IP address.
        - Allow inbound traffic on port range All (All ICMP - IPv4) from anywhere (0.0.0.0/0). For both instances.
    - Review and launch the instance.

![Insatnce 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/1.%20Instance%201%20Settings%20.png?raw=true)  

![SG 1 Inbound](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/2.%20SG%20Inbound%20rules.png?raw=true)  

#### Insatace 1

![Insatnce 2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/3.%20Instance%202%20%20Settings%20.png?raw=true)  

![SG 2 Inbound](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/4.%20SG%20Inbound%20rules.png?raw=true)  

#### Instance 2

### 33. Set UP Flow Logs

1. **Go to the CloudWatch**:  
   - Check the Region and proceed.
2. **Create Log Group**:
   - Click on "Log groups" in the left sidebar.
   - Click on "Create log group".
   - Name the log group as `MyOrgVPCFlowLogsGroup`.
   - Click "Create".
   - Head back to the VPC Dashboard.
   - Select the VPC `MyOrg VPC-1`.
   - Scroll down to the "Flow Logs" section.
  
![Log group](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/5.%20Log%20group%20.png?raw=true)  

3. **Create Flow Log**:
    - Click on "Create flow log" from VPC Dashboard for `MyOrg VPC-1`.
    - Name: `MyOrgVPCFlowLog`.
    - Filter: `All`.
    - Maximum aggregation interval: `1 minute`.
    - Destination: `Send to a CloudWatch Logs group`.
    - Log Group: Select `MyOrgVPCFlowLogsGroup`.
    - IAM Role: Create a new role with the name `MyOrgVPCFlowLogsRole`.

![Flow log](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/6.%20Flow%20Log%20for%20VPC%201.png?raw=true)  

![flow log](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/6.1,12.%20Create%20a%20flow%20log.png?raw=true)  

#### 34. Create IAM Role for Flow Logs :

  - Go to the IAM Dashboard in New tab(prefer).
  - Click on "Policies" in the left sidebar.
  - Click on "Create policy".
  - Chose the "JSON" tab.
  - Delete the default content and paste the following policy:  

```json
{
   "Version": "2012-10-17",
   "Statement": [
      {
         "Effect": "Allow",
         "Action": [
            "logs:CreateLogGroup",
            "logs:CreateLogStream",
            "logs:PutLogEvents",
            "logs:DescribeLogGroups",
            "logs:DescribeLogStreams"
         ],
         "Resource": "*"
      }
   ]
}
```

  - Choose Next
  - Name the policy as `MyOrgVPCFlowLogsPolicy`.
  - Click "Create policy".

![Policy](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/7.%20IAM%20flow%20log%20policy.png?raw=true)  

  - Now Choose **Roles** on left hand navigation pane.
  - Click on "Create role".
  - Select "Custom Trust policy" as the trusted entity type.
  - replacle "principal" with the following:

```json
  {
    "Service": "vpc-flow-logs.amazonaws.com"
  }
```

  - Choose Next.
  - On add permissions page, search for the policy `MyOrgVPCFlowLogsPolicy` and select it.
  - Click Next.
  - Name the role as `MyOrgVPCFlowLogsRole`.
  - Click "Create role".

![Role](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/8.%20IAM%20role%20for%20Flow%20log.png?raw=true)  

![Role 2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/9.%20Custom%20Trust%20policy%20code.png?raw=true)  

![Role 3](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/10.%20Flow%20Log%20Policy%20Permission.png?raw=true)  

![Role 4](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/11.%20Name%20of%20the%20Flow%20Log%20Role.png?raw=true)  

Now go back to the VPC Dashboard.

---

### 33. Continuation of Set up Flow Logs:

  - Select the IAM role `MyOrgVPCFlowLogsRole`.
  - Click "Create flow log".
  - Now FFlow Log is all setup.  
    
![](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/6.1,12.%20Create%20a%20flow%20log.png?raw=true)  

![last](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/12.%20Set%20up%20to%20create%20Fow%20Log.png?raw=true)  

---

### 34. Test VPC Peering Connection

1. **Check VPC Peering Connection Status**:
  - Go to the VPC Dashboard.
  - Click on "Peering Connections" in the left sidebar.
  - Select the peering connection `VPC 1 <> VPC 2`.
  - Ensure the status is `Active`.
2. **Test Connectivity**:
  - Go to the EC2 Dashboard.
  - Select the instance `Instance - MyOrg VPC 1`.
  - Click on "Connect" and choose "Session Manager".
  - In the terminal, run the following command to test connectivity to the instance in VPC 2:   

```bash
  ping <Private IP of Instance - MyOrg VPC 2>
  ```

- If you receive responses, the peering connection is working correctly.

![test](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/13.%20Test%201.png?raw=true)  

  - See if you can test the connection from VPC 1 to VPC 2's public IP address.
  - Head back to your EC2 console, and copy the Public IPv4 address of Instance - NextWork VPC 2.
  - Your final result should look similar to something like 

```bash
  ping <public IPv4 address>
  ```

- If you receive responses, the peering connection is working correctly.

![test 2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/14.%20Test%202%20.png?raw=true)  

- If Got any error please check the following:
  - Ensure that the security groups and network ACLs allow traffic between the two VPCs.
  - Check the route tables in both VPCs to ensure they have routes for the peered VPC's CIDR block.
  - my suggestion is to check the previous project that is [VPC Peering Connection]then you can find the solution.

- If you got everything right, thats good you have successfully completed the project.
- Now you may test some another extension as an option.
-Another optional extension! Back in your EC2 Instance Connect tab, run the same ping command but add -c 5 to the end of the command.  

```bash
  ping [Private IP of Instance - MyOrg VPC 2] -c 5
```

![test 3](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/15.%20Test%203.png?raw=true)  

- you should see 5 pings sent and automatically finish after 5 packets, which means the peering connection is working correctly.


![last test](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/16.%20last%20test.png?raw=true)  

---

### 35. Analyze Flow Logs

- Head to your CloudWatch console.
- Click on "Log groups" in the left sidebar.
- Select the log group `MyOrgVPCFlowLogsGroup`.
- Click into your log stream to see flow logs from EC2 Instance 1
- You should see logs similar to the following:  

  ```
  2023-10-01T12:00:00.000Z MyOrgVPCFlowLog 1234567890123456 1234567890123456 eni-1234567890abcdef    
  ACCEPT OK
  ```

![log groups](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/17.%20LogGroups.png?raw=true)  

- The log entries will contain information about the traffic flowing through the VPC, including source and destination IP addresses, ports, and protocols.
- You can use these logs to monitor and analyze network traffic, troubleshoot issues, and ensure compliance with security policies.
- In the left hand navigation panel, click on Logs Insights.
- Select the log group `MyOrgVPCFlowLogsGroup` from the select log group dropdown.
- select the Query folder on the right hand size.
- Under Flow Logs, select Top 10 byte transfers by source and destination IP addresses.
- Click Apply, and then Run query.
- Review the query results.

![log sights 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/18.%20Log%20Insights%201.png?raw=true)  

![log sights 2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/19.%20Log%20Sights%202.png?raw=true)  


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

