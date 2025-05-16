
# AWS Cloud Security Project

This project demonstrates the implementation of cloud security best practices using AWS services like **EC2**, **IAM Policies**, **IAM Users**, **IAM Groups**, and **Account Alias**. It secures access to EC2 instances based on environment tags using IAM policies.

---

## 🚀 Project Objectives

- Launch and secure EC2 instances for **Development** and **Production** environments.
- Create IAM policies to allow access to specific resources based on tags.
- Assign IAM users to respective IAM groups and restrict their access accordingly.
- Set a custom AWS account alias for user login.

---

## 🏗️ Project Architecture

| Component        | Development                    | Production                    |
|------------------|--------------------------------|-------------------------------|
| EC2 Instance     | `myorg-development-vd`         | `myorg-production-vd`         |
| EC2 Tag          | `env=Development`              | `env=Production`              |
| IAM Policy       | `MyOrgDevEnvPolicy`            | `MyOrgProdEnvPolicy`          |
| IAM Group        | `myorg-development-group`      | `myorg-production-group`      |
| IAM User         | `myorg-dev-vd`                 | `myorg-prod-vd`               |
| Account Alias    | `myorg-interns`                | -                             |

insert image here:
![Project Architecture](https://github.com/guntupallivasudeva/AWS_Beginner_level_projects/blob/main/Aws%20Cloud%20Security%20Using%20EC2,%20IAM%20Policies,%20IAM%20Users%20Groups%20and%20Users%20&%20Account%20Alias%20/Images/Project%20Architeture.png?raw=true)
---

## ✅ Step-by-Step Implementation

### 1️⃣ Launch EC2 Instances

- Go to **EC2 Dashboard → Launch Instance**
  - Name: myorg-development-vd  
  - Tag: Key: env, Value: Development  
  - AMI: Amazon Linux 2  
  - Instance Type: t2.micro  
  - Key Pair: Create or use existing  
  - Security Group: Allow SSH (port 22)  
  - Remaining settings as default  
- Click Launch Instance  
- Repeat the above steps for the Production instance:  
  - Name: myorg-production-vd  
  - Tag: Key: env, Value: Production   

- **Instance 1**:  
  - Name: `myorg-development-vd`  
  - Tag: `env = Development`  
 
---

- Go to **EC2 Dashboard → Launch Instance**
  - Name: myorg-development-vd  
  - Tag: Key: env, Value: Development  
  - AMI: Amazon Linux 2  
  - Instance Type: t2.micro  
  - Key Pair: Create or use existing  
  - Security Group: Allow SSH (port 22)  
  - Remaining settings as default  
- Click Launch Instance   

- **Instance 2**:  
  - Name: `myorg-production-vd`  
  - Tag: `env = Production`  

---

### 2️⃣ Create IAM Policies

- To create the policy, follow these steps:  
- Go to IAM → Policies → Click Create policy  
- Go to the JSON tab  
- Paste your policy JSON, e.g. for development environment:  

#### 📄 MyOrgDevEnvPolicy

```json
{    
  "Version": "2012-10-17",    
  "Statement": [        
    {            
      "Effect": "Allow",            
      "Action": "ec2:*",            
      "Resource": "*",            
      "Condition": {                
        "StringEquals": {                    
          "ec2:ResourceTag/Env": "Development"                
        }            
      }        
    },        
    {            
      "Effect": "Allow",            
      "Action": "ec2:Describe*",            
      "Resource": "*"        
    },        
    {            
      "Effect": "Deny",            
      "Action": [                
        "ec2:DeleteTags",                
        "ec2:CreateTags"            
      ],            
      "Resource": "*"        
    }    
  ] 
}

```
- Click Next → Add a name: MyOrgDevEnvPolicy
- Click Create policy  
✅ Policy is now ready to attach.

#### 📄 MyOrgProdEnvPolicy

- To create the policy, follow these steps:   
- Go to IAM → Policies → Click Create policy  
- Go to the JSON tab  
- Paste your policy JSON, e.g. for Production environment:  

```json
{    
  "Version": "2012-10-17",    
  "Statement": [        
    {            
      "Effect": "Allow",            
      "Action": "ec2:*",            
      "Resource": "*",            
      "Condition": {                
        "StringEquals": {                    
          "ec2:ResourceTag/Env": "Production"                
        }            
      }        
    },        
    {            
      "Effect": "Allow",            
      "Action": "ec2:Describe*",            
      "Resource": "*"        
    },        
    {            
      "Effect": "Deny",            
      "Action": [                
        "ec2:DeleteTags",                
        "ec2:CreateTags"            
      ],            
      "Resource": "*"        
    }    
  ] 
}

```
- Click Next → Add a name: MyOrgProdEnvPolicy  
- Click Create policy  
✅ Policy is now ready to attach.
---

### 3️⃣ Create IAM Groups

- **myorg-development-group** 
1. Create IAM User Group  
2. Go to the AWS Console → Search for IAM → Click User Groups  
3. Click "Create group"  
4. Group name: myorg-development-group    
5. Attach policies   
6. You can attach custom policy before you MyOrgDevEnvPolicy.  
Click "Create group"   

✅ Your IAM group is now created. 
  - Attached to `MyOrgDevEnvPolicy`

- **myorg-production-group**  
1. Create IAM User Group  
2. Go to the AWS Console → Search for IAM → Click User Groups  
3. Click "Create group"  
4. Group name: myorg-production-group  
5. Attach policies    
6. You can attach custom policy before you MyOrgProdEnvPolicy.  
Click "Create group"  
  - Attached to `MyOrgProdEnvPolicy`

---

### 4️⃣ Create IAM Users

- **myorg-dev-vd**  
1. Create IAM User and Add to Group
2. Go to IAM → Users → Click Add users
3. User name: myorg-dev-vd (or any name)
4. Check ✅ "Provide user access to the AWS Management Console"
5. Set a custom password(recommended)
6. uncheck Require password reset on first sign-in
7. Click Next → Add user to group
8. Select the group: myorg-development-group
9. Click Next → Review → Create user

✅ IAM user is created and inherits the group policy.
  - Add to group: `myorg-development-group`

- **myorg-prod-vd**  
1. Create IAM User and Add to Group
2. Go to IAM → Users → Click Add users
3. User name: myorg-prod-vd (or any name)
4. Check ✅ "Provide user access to the AWS Management Console"
5. Set a custom password(recommended)
6. Uncheck Require password reset on first sign-in
7. Click Next → Add user to group
8. Select the group: myorg-production-group
9. Click Next → Review → Create user

✅ IAM user is created and inherits the group policy.
  - Add to group: `myorg-production-group`

- Set custom passwords and enable console access for both.

---

### 5️⃣ Set Account Alias

- Go to **IAM → Dashboard → Account Alias**
- Set alias: `myorg-interns`

Login URL for IAM users:
```
https://myorg-interns.signin.aws.amazon.com/console
```

---

### 6️⃣ Test IAM Access Controls

- Login as each user using the alias URL.    
- Use the custom password set during user creation.  
- **myorg-dev-vd**:  
  - URL: `https://myorg-interns.signin.aws.amazon.com/console`  
  - Username: `myorg-dev-vd`  
  - Password: (your custom password)   
- After logging in, go to **EC2 Dashboard**.  
- **myorg-dev-vd**:   
  - Try accessing EC2 instances.  
- Validate:  
  - `myorg-dev-vd` has access to Development instance only.  
  - `myorg-prod-vd` has denied to Production instance only.  

- **myorg-prod-vd**:  
  - URL: `https://myorg-interns.signin.aws.amazon.com/console`  
  - Username: `myorg-prod-vd`  
  - Password: (your custom password)  
- After logging in, go to **EC2 Dashboard**.  
- **myorg-prod-vd**:  
- Try accessing EC2 instances.  
- Validate:  
  - `myorg-dev-vd` has denied to Development instance only.  
  - `myorg-prod-vd` has access to Production instance only.  

---

## 🔐 Optional Enhancements

- ✅ Enable **Multi-Factor Authentication (MFA)** for users
- ✅ Enable **CloudTrail** to audit access logs
- ✅ Apply **least privilege principle** by restricting actions further
- ✅ Create **resource-based policies** using tags

---

## 📂 Project Structure Overview

```text
AWS Cloud Account:
├── EC2 Instances
│   ├── myorg-development-vd (Tag: env=Development)
│   └── myorg-production-vd (Tag: env=Production)
├── IAM Users
│   ├── myorg-dev-vd
│   └── myorg-prod-vd
├── IAM Groups
│   ├── myorg-development-group
│   └── myorg-production-group
├── IAM Policies
│   ├── MyOrgDevEnvPolicy
│   └── MyOrgProdEnvPolicy
└── Account Alias: myorg-interns
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
