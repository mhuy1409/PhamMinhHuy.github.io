---
title : "Create IAM Role"
date :  "2025-08-12T00:00:00+07:00"
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

### 1. Create IAM Role

Go to **IAM** (Identity and Access Management).

Select **Roles** > **Create role**.

![](/images/2-prerequiste/CRIAM.png)

Select **Trusted entity** type as **AWS service**.

Choose the use case as **EC2** and click **Next**.

![](/images/2-prerequiste/IMGIAM.png)

Search for and select the policy named `AmazonS3FullAccess`.  
Click **Next**.

![](/images/2-prerequiste/IAM3.png)

Click **Next: Review**.

Name the role `EC2S3AccessRole`.

Click **Create role**.

### 2. Attach IAM Role to EC2 Instance
Go to **EC2 console**.

Select **Instances** > Select the instance you are using.

Go to the **Actions** tab > **Security** > **Modify IAM Role**.

Select the role you just created **EC2S3AccessRole**.

Click **Save**.

![](/images/2-prerequiste/IAM4.png)

### 3. SSH Connection:

```
ssh -i mykey.pem ec2-user@<Public-IP>
```

**Public-IP** is the public IP address of the EC2 instance you are connecting to.  
**mykey.pem** is the key you used or created for EC2.

![](/images/2-prerequiste/SSH.png)

Install Samba (simulate SMB file server):

```
sudo yum update -y
sudo yum install samba samba-client -y
sudo mkdir /srv/files
sudo dd if=/dev/zero of=/srv/files/testfile1 bs=1M count=50
sudo dd if=/dev/zero of=/srv/files/testfile2 bs=1M count=100
```


### Content
  - [Create VPC and EC2](2.1.1-createvpc/)
  - [Create IAM Role](2.1.2-createpublicsubnet/)
