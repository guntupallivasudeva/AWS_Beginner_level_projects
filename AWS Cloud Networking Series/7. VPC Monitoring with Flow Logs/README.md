# 🌐 AWS VPC Setup Guide - MyOrg Configuration  

This guide provides a step-by-step process for creating a VPC Peering Connection between two VPCs in the **Asia Pacific (Hyderabad)** region (`ap-south-2`) using the AWS Console.

## VPC Monitoring with Flow Logs
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
- **VPC Peering Connection Description**: `Peering connection between MyOrg VPC-1 and MyOrg VPC-2` as VPC 1 <> VPC 2
- **VPC Flow Logs**: `MyOrgVPCFlowLogsGroup` & `MyOrgVPCFlowLog`
- **VPC Flow Log IAM Role**: `MyOrgVPCFlowLogsRole`
- **VPC Flow Log Policy**: `MyOrgVPCFlowLogsPolicy`


----
## 🚀 Project Overview
This project demonstrates how to set up VPC Peering Connections between two VPCs in AWS, enabling communication between resources in different VPCs. It includes the creation of VPCs, subnets, route tables, security groups, and EC2 instances, along with monitoring using VPC Flow Logs.

---

## 📘 Step-by-Step Instructions

(Previous setup steps for VPC, subnets, route tables, NACLs, Instances...)

---

## Project Architecture Diagram

![VPC Peering Architecture]()

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

![Insatnce 2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/3.%20Instance%202%20%20Settings%20.png?raw=true)  

![SG 2 Inbound](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/4.%20SG%20Inbound%20rules.png?raw=true)  

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
    ping -c 5 <Private IP of Instance - MyOrg VPC 2>
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
  ACCEPT OK```

![log groups](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/17.%20LogGroups.png?raw=true)  

- The log entries will contain information about the traffic flowing through the VPC, including source and destination IP addresses, ports, and protocols.
- You can use these logs to monitor and analyze network traffic, troubleshoot issues, and ensure compliance with security policies.
- In the left hand navigation panel, click on Logs Insights.
- Select the log group `MyOrgVPCFlowLogsGroup` from the select log group dropdown.
- select the Query folder on the right hand size.
- Under Flow Logs, select Top 10 byte transfers by source and destination IP addresses.
- Click Apply, and then Run query.
- Review the query results.

![log sights 1](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/18.%20Log%20Insights%201.png?raw=true)  

![log sights 2](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/7.%20VPC%20Monitoring%20with%20Flow%20Logs/Images/19.%20Log%20Sights%202.png?raw=true)  


---
----------------------------------------------------------
| Component        | Name                                |
|------------------|-------------------------------------|
| VPC              | `MyOrg VPC-1`                       |
|                  | `MyOrg VPC-2`                       |
| Subnet           | `MyOrg VPC-1 Public Subnet`         |
|                  | `MyOrg VPC-2 Public Subnet`         |
| Internet Gateway | `MyOrg VPC-1 IG`                    |
|                  | `MyOrg VPC-2 IG`                    |
| Route Tables     | `MyOrg VPC-1 Public Routetable`     |
|                  | `MyOrg VPC-2 Public Routetable`     |
| Security Groups  | `MyOrg VPC-1 Public SG`,            |
|                  | `MyOrg VPC-2 Public SG`             |
| Network ACLs     | `MyOrg VPC-1 Public Network ACL`    |
|                  | `MyOrg VPC-2 Public Network ACL`    |
| EC2 Instances    | `Instance - MyOrg VPC-1`            |
|                  | `Instance - MyOrg VPC-2`            |
| Log Groups       | `MyOrgVPCFlowLogsGroup`             |
|                  | `MyOrgVPCFlowLog`                   |
| IAM Roles        | `MyOrgVPCFlowLogsPolicy`            |
|                  | `MyOrgVPCFlowLogsRole`              |
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
├── Log Groups
│   └── MyOrgVPCFlowLogsGroup
│       └── MyOrgVPCFlowLog
├── IAM Roles & Policies
│   ├── MyOrgVPCFlowLogsPolicy
│   └── MyOrgVPCFlowLogsRole

```

----

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
