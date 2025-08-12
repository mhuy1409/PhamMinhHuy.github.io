---
title : "Tạo IAM Role"
date :  "2025-08-12T00:00:00+07:00"
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

### 1. Tạo IAM Role

Vào **IAM** (Identity and Access Management).

Chọn **Roles** > **Create role**.

![](/images/2-prerequiste/CRIAM.png)

Chọn loại **Trusted entity** là **AWS service**.

Chọn use case là **EC2** rồi nhấn **Next**

![](/images/2-prerequiste/IMGIAM.png)


Tìm kiếm và chọn policy có tên `AmazonS3FullAccess`.
Nhấn **Next**.


![](/images/2-prerequiste/IAM3.png)

Nhấn **Next: Review**.

Đặt tên role `EC2S3AccessRole`.

Nhấn **Create role**.


### 2. Gán IAM Role vào EC2 Instance
Vào **EC2 console**.

Chọn **Instances** > Chọn instance bạn đang dùng.

Chọn tab **Actions** > **Security** > **Modify IAM Role**.

Chọn role bạn vừa tạo **EC2S3AccessRole**

Nhấn **Save**.

![](/images/2-prerequiste/IAM4.png)

### 3. Kết nối SSH:


```
  ssh -i mykey.pem ec2-user@<Public-IP> 
```
**Public-IP** là địa chỉ IP công khai của máy chủ EC2 bạn đang kết nối.
**mykey.pem** là khóa bạn đã sử dụng hoặc tạo EC2.

![](/images/2-prerequiste/SSH.png)

Cài Samba (mô phỏng file server SMB):

```
sudo yum update -y
sudo yum install samba samba-client -y
sudo mkdir /srv/files
sudo dd if=/dev/zero of=/srv/files/testfile1 bs=1M count=50
sudo dd if=/dev/zero of=/srv/files/testfile2 bs=1M count=100
 
```




### Nội dung
  - [Tạo VPC và EC2](2.1.1-createvpc/)
  - [Tạo IAM Role](2.1.2-createpublicsubnet/)

