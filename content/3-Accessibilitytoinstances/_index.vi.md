---
title : "Tạo AWS Storage Gateway"
date :  "2025-08-12T00:00:00+07:00"
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
1. Vào **AWS Storage Gateway → Create gateway**.

![](/images/3.connect/Gateway3.png)

2.  Đặt tên: `WS-SG`

 Chọn:
   - Gateway type: **Amazon S3 File Gateway**
   - Host platform: **Amazon EC2** hoặc on-premises VM.

![](/images/3.connect/gateway.png)

3. Chọn **VPC/Subnet** giống EFS và S3.
4. Lấy **Activation Key** → **Activate Gateway**.


![](/images/3.connect/Gateway2.png)

6. Connect to AWS Gateway connection options

+ Chọn **IP address**.

+ **Endpoint options**: chọn **Publicly accessible**: cho phép Storage Gateway giao tiếp với AWS qua internet.


+ Nhấn **Next** để sang bước tiếp theo.

![](/images/3.connect/Gateway4.png)

7. Ở bước tiếp theo kiểm tra và chọn **Activate gateway**
8. Bước 4 **Configure gateway**

+ **CloudWatch log group** chọn **Create a new log group**
+ **CloudWatch alarms** chọn **Create Storage Getaway's recommended alarms**
+ Ấn **Configure**
![](/images/3.connect/Gateway5.png)