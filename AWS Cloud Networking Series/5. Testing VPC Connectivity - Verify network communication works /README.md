# 🌐 AWS VPC Setup Guide - MyOrg Configuration  
##  Testing VPC Connectivity - Verify network communication works  
---

## 📘 Step-by-Step Instructions

(Previous setup steps for VPC, subnets, route tables, NACLs...)

---

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

![Internet Connectivity](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/AWS%20Cloud%20Networking%20Series/5.%20Testing%20VPC%20Connectivity%20-%20Verify%20network%20communication%20works%20/Images/8.%20Final%20Connectivity.png?raw=true)

**Thats It we Done with Connectivity Check**  

---

## ✅ Final Updated Summary

----------------------------------------------------------
| Component        | Name                                |
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

----
