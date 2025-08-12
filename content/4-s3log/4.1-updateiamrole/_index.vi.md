---
title : "Tạo AMAZON EFS"
date :  "2025-08-12T00:00:00+07:00"
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

1. Tìm và chọn vào **EFS** ->  **Create file system**

![](/images/4.s3/EFS1.png)

2. Đặt tên `Workshop-EFS`
+ Chọn VPC Wordshop của bạn: **Workshop-VPC**
+ Nhấn vào **Customize**

![](/images/4.s3/EFS2.png)

3. Ở bước 1:
+ **File system type** chọn **Regional**
+ **Transition into IA** chọn **30 days**
+ **Transition into Archive** chọn **None**
+ **Throughput mode** chọn **Bursting**.
+ Bấm **Next**


![](/images/4.s3/EFS3.png)


Bước 2: **Network Access:**

+ Chọn VPC: Workshop-VPC
+ Tạo Mount Target cho **ap-southeast-1a** với subnet tương ứng.
+ Gắn Security Group mở port 2049.



![](/images/4.s3/EFS4.png)

Bước 3. **File system policy**: để mặc định và bấm **Next**

Bước 4. **Review and Create** kiểm tra rồi bấm **Create file system**.

![](/images/4.s3/EFS5.png)


