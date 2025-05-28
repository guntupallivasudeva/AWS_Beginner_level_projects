
# 📘 AWS Console Setup Guide: Access S3 With VPC Endpoint

## ✅ Prerequisites
- An IAM user with administrative privileges
- Logged into AWS Console in a supported browser
- Region: `Asia Pacific (Hyderabad)` (or your preferred)

---

## 🛠️ Steps to Create VPC, EC2, S3, and VPC Endpoint:

## Project Architecture

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/PA%201%20.png?raw=true) 

before adding Endpoint and S3 bucket policy, the architecture looks like this

![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/PA%202%20.png?raw=true)

After adding Endpoint and S3 bucket policy, the architecture looks like this

---

### 1. **Create VPC (MyOrg VPC)**  

1. Go to **VPC Dashboard** 
→ **Your VPCs** → **Create VPC**
2. Choose: `VPC & more`
  - Name tag auto-generation : `MyOrg`
  - IPv4 CIDR: `10.0.0.0/16`
  - Tenancy: `Default`
  - Number of Availability Zones: `1`
  - Number of public subnets: `1`
  - Number of private subnets: `0`
  - NAT gateways: `none`
  - VPC endpoint: `none`
  - Leave IPv6, DNS settings as default
3. Click **Create VPC**

![1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/1.%20VPC%20create.png?raw=true)

-

![2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/2.%20VPC%20create.png?raw=true)

-

![3](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/3.%20VPC%20create.png?raw=true)

-

![4](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/4.%20VPC%20Resource%20Map.png?raw=true)

-

![5](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/5.%20VPC%20created.png?raw=true)


---

### 2 **Launch EC2 Instance**
  
1. Go to **EC2 > Instances > Launch instance**
2. Name: `Instance - MyOrg VPC`
  - AMI: Amazon Linux 2023 AMI
  - Instance type: `t3.micro` (free tier eligible)
  - Key Pair: Proceed with out a keypair(not recommended)
3. **Network Settings**:
  - VPC: `MyOrg-vpc`
  - Subnet: `MyOrg Public Subnet`
  - Auto-assign IP: Enabled
  - Security Group: Create Security Group >
  - name:`SG - MyOrg Insatance`
4. Click **Launch Instance**

![6](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/6.%20EC2%20Instace%202.png?raw=true)

-

![7](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/7.%20EC2%20Instace%203.png?raw=true)

-

![8](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/8.%20EC2%20Instace%204.png?raw=true)

-

![9](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/9.%20EC2%20Instace%205.png?raw=true)


---

### 3. **Create S3 Bucket**  

1. Go to **S3 Dashboard** → **Create Bucket**
2. Bucket type: `General purpose`
3. Name: `myorg-vpc-endpoints-vasu`
4. Leave other settings as default
5. Click **Create Bucket**

![10](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/10.%20Create%20Bucket.png?raw=true)

-

![11](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/11.%20Upload%20Files%20to%20Bucket.png?raw=true)


6. **Upload 2 Files to Bucket**
  - Open the bucket Click on - **Upload** 
  - Select Add Files 
  - Select two files from computer
  - `1.png` and `2.png`(in my case)
  - Click **Upload**

---
### 4. **Connect to your EC2 Instance**  

1. Go to **EC2 Dashboard > Instances**
2. Select checkbox next to `Instance - MyOrg VPC`
3. Click **Connect**
4. Leave Default Selection in connect to instance tab
5. Click **Connect** button
6. You will be connected to the instance via AWS CLI
7. now you see this type of interface
8. run the command:

```bash
ping [private IP of Instance]
```

9. You should see a response indicating the instance is reachable like this:

![12](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/12.%20Connect%20your%20Ec2.png?raw=true)

10. now we back to console to create IAM user and access key

---

### 5. **Create IAM Access Key for Admin**

1. Go to **IAM** Dashboard 
  - If your on user account
  - Search in IAM dashboard as access keys
  - Then select the displayed option
  - Then click on **Create access key**
2. If you are on root account
  - Go to right top corner
  - Click on your account name
  - Click on **My Security Credentials**
  - Then Click on Access keys

3. Click **Create access key**
4. Choose Use case as Command line Interface (CLI)
5. Tick check box for `I understand the above recommendation and want to proceed to create an access key`
6. Click **Next**
7. paste description as `Access key created to access an S3 bucket from an EC2 Instance. NextWork VPC Endpoints project`.
8. Click **Create access key**
9. Download the `.csv file`.

![13](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/13.%20IAM%20Access%20Key%201.png?raw=true)

-

![14](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/14.%20IAM%20Access%20Key%202.png?raw=true)

-

![15](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/15.%20IAM%20Access%20Key%203.png?raw=true)

---
### 6. **Connect to your S3 bucket**

1. Open EC2 Instance Connect Tab.
2. Run the following command :

```bash
aws configure
```
3. Enter the following details when prompted:

```plaintext
AWS Access Key ID [None]: <Your Access Key ID>
AWS Secret Access Key [None]: <Your Secret Access Key>
Default region name [None]: ap-south-2
Default output format [None]: Leave blank

```
![16](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/16.%20Congfiure.png?raw=true)

4. Now run the following command to list the S3 buckets:

```bash
aws s3 ls
```

![17](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/17.%20S3%20ls.png?raw=true)

5. You should see the `myorg-vpc-endpoints-bucket` listed. 
6. To access the files in the bucket, run:

```bash
aws s3 ls s3://myorg-vpc-endpoints-vasu
```

![18](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/18.%20files%20in%20bucket%20.png?raw=true)

7. You should see the files `1.png` and `2.png` listed.
8. Now you can upload the files using CLI from the following command:
  
```bash
sudo touch /tmp/myorg-file.txt
```
9. it create a blank .txt file in your EC2 Instance.
10. Now run the following command to upload the file to S3 bucket:

```bash
aws s3 cp /tmp/myorg-file.txt s3://myorg-vpc-endpoints-vasu/
```

![19](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/19.%20new%20file%20add.png?raw=true)

11. To verify the upload, run:

```bash
aws s3 ls s3://myorg-vpc-endpoints-vasu/
```

![20](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/20.%20FIles%20Verify.png?raw=true)

12. You should see `myorg-file.txt` listed in the bucket by Switching back to S3 Console in another tab.

![21](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/21.%20verify%20in%20s3%20bucket.png?raw=true)

13. Leave the connection tab open and proceed to create VPC Endpoint in another new tab.

---

### 7. **Create VPC Endpoint for S3**

1. Go to **VPC Dashboard**
2. click on Endpoints on Left nav > **Create Endpoint**
3. name: `MyOrg VPC Endpoint`
4. Service category: `AWS services`
5. Service name: `com.amazonaws.ap-south-2.s3`
6. Select the Type: `Gateway`
7. VPC: `MyOrg-vpc`
8. Route Table: Select `MyOrg Public Route Table`
9. Policy: Leave as `Full Access` (or customize)
10. Click **Create Endpoint**
11. Wait for the endpoint to be created
12. Once created, you will see the endpoint in the list with a status of `Available`

![22](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/22.%20Create%20Endpoint.png?raw=true)

-

![23](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/23.%20Create%20Endpoint%202.png?raw=true)

-

![24](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/24.Create%20Endpoint%202%20.png?raw=true)

-

![25](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/25.%20Create%20Endpoint%203.png?raw=true)

-

![26](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/26.%20%20Add%20route%20table%20to%20endpoint.png?raw=true)

-

![27](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/27.%20Endpoint%20added%20to%20route%20table.png?raw=true)

-

![28](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/28.%20Endpoint%20Created.png?raw=true)

---

### 8. **Add S3 Bucket Policy to Allow Access via VPC Endpoint**  

1. Go to **S3 Dashboard**
2. Click on `myorg-endpoint-vasu` 
3. Again Chooses Permissions Tab
4. Click on `Bucket Policy` and then click on `Edit` button
5. Add the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::myorg-endpoint-vasu",          //replace with your bucket name
        "arn:aws:s3:::myorg-endpoint-vasu/*"       //replace with your bucket name
      ],
      "Condition": {
        "StringNotEquals": {
          "aws:SourceVpce": "vpce-xxxxxxxxxxxxxxxxx"        //replace with your VPC endpoint ID
        }
      }
    }
  ]
}
```

![policy pic](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/29%20.%20S3%20Policy.png?raw=true)

3. Replace bucket name and vpce id `vpce-xxxxxxxxxxxx` with your actual VPC endpoint ID
4. Use above Bucket ARN on top and VPC Endpoint ID in the Vpc endpoint tab.
5. Save changes
6. if you got any error, the make sure the route table is allowing the traffic to the S3 endpoint
7. go to the vpc endpoint tab and check the route table and modify to add the `MyOrg-rtb-public` route table.
8. now check back the routes that the route table has the following routes:
  - Destination: `pl-xxxxxxxxxxxx` (S3 prefix list)
  - Target: `vpce-xxxxxxxxxxxx` (your VPC endpoint ID)
9. Now you can access the S3 bucket from the EC2 instance using the VPC endpoint.
10. now check the S3 bucket from the EC2 instance using the following command: in the EC2 instance Connect tab

```bash
aws s3 ls s3://myorg-endpoint-vasu/
```
11. You can find the files you uploaded earlier in the S3 bucket.

![30](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/8.%20Accessing%20S3%20with%20VPC%20Endpoint/Images/30.%20All%20in%20one%20verify.png?raw=true)

---

### 9. Components Table

----------------------------------------------------------
| Component        | Name                                |
|------------------|-------------------------------------|
| VPC              | `MyOrg-vpc`                         |
| Subnet           | `MyOrg-vpc-subnet-public1`          |         
| Internet Gateway | `MyOrg-ig`                          |
| Route Tables     | `MyOrg-rtb-public`                  |
| Security Groups  | `SG - MyOrg Instance`               |
| Network ACLs     | `MyOrg-vpc-public-network-acl`      |
| EC2 Instances    | `Instance - MyOrg VPC`              |
| S3 Bucket        | `myorg-endpoint-vasu`               |
| VPC Endpoint     | `MyOrg S3 Endpoint`                 |
----------------------------------------------------------

--- 

### 10. 📂 Final Project Structure Overview

```text

AWS Cloud Account:
├── VPC
│   └── MyOrg-vpc
├── Subnets
│   └── MyOrg-subnet-public1
├── Internet Gateway
│   └── MyOrg-vpc-ig
├── Route Tables
│   └── MyOrg-vpc-public-rt
├── Security Groups
│   └── MyOrg-vpc-public-sg
├── Network ACLs
│   └── MyOrg-vpc-public-network-acl  
├── EC2 Instances
│   └── Instance - MyOrg VPC
├── S3 Bucket
│   └── MyOrg-vpc-endpoints-vasu
├── VPC Endpoints
│       └── MyOrg-vpc-endpoint
├── IAM User
│   ├── MyOrg-Admin-User
│   └── MyOrg-Admin-Access-Key
```
---

### ✅ Final Output
- VPC: `MyOrg-vpc`
- Subnet: `MyOrg-subnet-public1`
- EC2: `Instance - MyOrg VPC`
- SG: `SG - MyOrg Instance`
- S3: `myorg-endpoint-vasu`
- VPC Endpoint: `MyOrg S3 Endpoint`
- Verified access via AWS CLI from EC2 to S3 using the endpoint

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
