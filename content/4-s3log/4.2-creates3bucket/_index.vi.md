---
title : "Tạo S3 Bucket"
date :  "2025-08-12T00:00:00+07:00"
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---



### 1. Tạo **S3 Bucket**

Vào **AWS Management Console** → **S3** → **Create bucket**.
![](/images/4.s3/S3.png)

**Cấu hình:**

+ **Bucket name:** ``workshop-s3-gateway``
(Tên này cần khớp với phần cấu hình Storage Gateway sau này.)

+ AWS Region: **Asia Pacific (Singapore) ap-southeast-1** (trùng region của Storage Gateway).

+ **Bucket type** chọn **General purpose**.

+ **Object Ownership** chọn **Bucket owner enforced (ACLs disabled)**.

+ **Block Public Access** Bật **Block all public access** (khuyến nghị để an toàn).

![](/images/4.s3/S31.png)

+ **Versioning** chọn **Disable** (trừ khi muốn lưu nhiều phiên bản).

+ **Bucket Key** chọn **Enable.**

+ Bấm **Create bucket**.

![](/images/4.s3/S32.png)

### 2. Tạo File Share
1. Quay lại Storage Gateway → chọn gateway Workshop-S3-Gateway.

+ Chọn vào **WS-SG** sau đó ấn vào **Create file share**.

+ **Gateway:** `WS-SG`

+ **Amazon S3 bucket** chọn **workshop-s3-gateway**.

+ **Access protocol**: Chọn **NFS** hoặc **SMB** (Windows nên chọn **SMB**).

+ Bấm **Create file share**.

![](/images/4.s3/S33.png)