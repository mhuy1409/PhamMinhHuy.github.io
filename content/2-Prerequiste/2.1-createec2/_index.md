---
title : "Create VPC and EC2"
date :  "2025-08-12T00:00:00+07:00"
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

### 1. Create VPC

1. Go to **AWS Console** → Search for **VPC** → **Create VPC**.

![](/images/2-prerequiste/CRVPC.png) 

2. Select **VPC only**.

3. Enter:
  + IPv4 CIDR block: **10.0.0.0/16**
  + Name tag: `Workshop-VPC`
  + Click **Create VPC**.

![](/images/2-prerequiste/VPCst.png)

5. In the VPC menu, select **Subnets** → **Create subnet**:

![](/images/2-prerequiste/CRSubnet.png) 

  + Name: `Public-Subnet`
  + VPC: **Workshop-VPC**
  + AZ: Choose any
  + CIDR block: 10.0.1.0/24
  
![](/images/2-prerequiste/stSubnet.png) 

Click **Add new subnet**:

 + Name: `Private-Subnet`
 + CIDR block: **10.0.2.0/24**

Click **Create subnet**.

![](/images/2-prerequiste/stSubnet2.png)

6. Go to **Internet Gateways** → **Create internet gateway**:
 + Name: `Workshop-IGW`
 + Click **Create**.

![](/images/2-prerequiste/IGst5.png)
Select **Attach to VPC** → **Workshop-VPC**.
![](/images/2-prerequiste/IGst3.png)

7. Go to **Route tables**:
Select the route table for **Public-Subnet** → **Edit routes** → **Add route**  
+ Destination: **0.0.0.0/0**
+ Target: Select **Internet Gateway** → **Workshop-IGW**.

![](/images/2-prerequiste/Editroutes.png)


### 2. Create EC2

1. Go to **EC2** → **Launch instance**:

![](/images/2-prerequiste/EC2.png)

+ Name: `Workshop-EC2`
+ AMI: Choose **Amazon Linux 2023 (kernel-6.1)**
+ Instance type: **t2.micro** (Free tier)
+ Key pair: Choose an existing key pair or create a new one (for SSH access)

![](/images/2-prerequiste/STEC3.png)

**Network settings:**
+ VPC: Select the **VPC** you created
+ Subnet: Choose **Public Subnet** (for SSH and package downloads)
+ Auto-assign public IP: **Enable**

**Security Group:**

Create a new one or select an existing one, ensuring at least:

+ SSH: TCP 22 (allow from your IP)
+ NFS: TCP 2049 inbound from the VPC or your IP

Click **Launch instance**.

![](/images/2-prerequiste/STEC2.png)

### Contents
  - [Create VPC and EC2](2.1.1-createvpc/)
  - [Create IAM Role](2.1.2-createpublicsubnet/)
