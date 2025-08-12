---
title : "Tạo VPC và EC2"
date :  "2025-08-12T00:00:00+07:00"
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

### 1. Tạo VPC

1.Vào **AWS Console** → Tìm **VPC** → **Create VPC**.

![](/images/2-prerequiste/CRVPC.png) 

2. Chọn **VPC only**.

3. Nhập:
  + IPv4 CIDR block: **10.0.0.0/16**
  + Name tag: `Workshop-VPC`
  + Bấm **Create VPC**.

![](/images/2-prerequiste/VPCst.png)

5. Trong menu VPC, chọn **Subnets** → **Create subnet**:

![](/images/2-prerequiste/CRSubnet.png) 


  + Name: `Public-Subnet`
  + VPC: **Workshop-VPC**
  + AZ: Chọn bất kỳ
  + CIDR block: 10.0.1.0/24
  
![](/images/2-prerequiste/stSubnet.png) 

Bấm **Add new subnet**:

 + Name: `Private-Subnet`
 + CIDR block: **10.0.2.0/24**

Bấm **Create subnet**.

![](/images/2-prerequiste/stSubnet2.png)

6. Vào **Internet Gateways** → **Create internet gateway**:
 + Name: `Workshop-IGW`
 + Bấm **Create**.

![](/images/2-prerequiste/IGst5.png)
Chọn **Attach to VPC** → **Workshop-VPC**.
![](/images/2-prerequiste/IGst3.png)

7. Vào **Route tables**:
Chọn route table của **Public-Subnet** → **Edit routes** → **Add route** 
+ Destination: **0.0.0.0/0**
+ Target: Chọn **Internet Gateway** → **Workshop-IGW**.

![](/images/2-prerequiste/Editroutes.png)


### 2. Tạo EC2

1. Vào **EC2** → **Launch instance**:

![](/images/2-prerequiste/EC2.png)

+ Name: `Workshop-EC2`.
+ AMI: Chọn **Amazon Linux 2023 (kernel-6.1)**.
+ Instance type: **t2.micro** (Free tier).
+ Key pair: Chọn key pair có sẵn hoặc tạo mới (để SSH vào).

![](/images/2-prerequiste/STEC3.png)

**Network settings:**
+ VPC: Chọn **VPC** mà bạn đã tạo.
+ Subnet: Chọn **Public Subnet** (để SSH và tải gói dễ).
+ Auto-assign public IP: **Enable**.

**Security Group:**

Tạo mới hoặc chọn sẵn, cần mở ít nhất:

+ SSH: TCP 22 (cho phép từ IP của bạn)
+ NFS TCP 2049 inbound từ VPC hoặc IP bạn

Nhấn **Launch instance**.

![](/images/2-prerequiste/STEC2.png)

### Nội dung
  - [Tạo VPC và EC2](2.1.1-createvpc/)
  - [Tạo IAM Role](2.1.2-createpublicsubnet/)

