+++
title = "Testing"
date = 2021
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

### 1. Test Mounting NFS from Storage Gateway

1. Run this bash command via SSH:

```
mount | grep /mnt/workshop
```

![](/images/6.clean/1.png)

This means:
+ The EC2 instance is connected to Storage Gateway via NFS.
+ You can read/write files inside `/mnt/workshop`.
+ Any file operations in this directory will sync to S3 via Storage Gateway.

![](/images/6.clean/2.png)

2. Check the mounted directory:

```
ls -l /mnt/workshop
```

![](/images/6.clean/3.png)

### 2. Test Reading and Writing Files from EC2 to Storage Gateway

1. Create a new file:

```
echo "Hello from EC2" | sudo tee /mnt/workshop/filetest1_from_ec2.txt
```

2. Check the newly created file:

```
ls -l /mnt/workshop/filetest1_from_ec2.txt

cat /mnt/workshop/filetest1_from_ec2.txt
```

![](/images/6.clean/4.png)

### 3. Test Syncing Storage Gateway Data with S3 Bucket

Check in the **AWS S3** console under bucket **workshop-s3-gateway** to ensure the file `filetest1_from_ec2.txt` appears.

![](/images/6.clean/5.png)

### 4. Test Direct Upload from EC2 to S3 (using IAM Role)

1. Create a file:

```
echo "Hello direct S3 upload" > filetest1_s3.txt
```

2. Upload to S3:

```
aws s3 cp filetest1_s3.txt s3://workshop-s3-gateway/
```

3. Verify the uploaded file:

```
aws s3 ls s3://workshop-s3-gateway/filetest1_s3.txt
```

![](/images/6.clean/6.png)

### 5. Test Writing File from On-Premises Machine to Storage Gateway

1. Create a test file:

```
echo "Hello from on-prem" > /mnt/workshop/filetest1_from_onprem.txt
```

2. Check this file on EC2:

```
ls -l /mnt/workshop/filetest1_from_onprem.txt

cat /mnt/workshop/filetest1_from_onprem.txt
```

![](/images/6.clean/7.png)

### 6. Test Deleting Files on Storage Gateway and Syncing to S3

1. Delete the file on EC2:

```
sudo rm /mnt/workshop/filetest4.txt
```

2. Check on the S3 bucket if the file is deleted:

```
aws s3 ls s3://workshop-s3-gateway/filetest4.txt
```

If the file is missing, it means deletion synced correctly.

### 7. Test Creating and Accessing Files on EFS

1. Mount EFS:

```
sudo mount -t nfs4 -o nfsvers=4.1 fs-09848ebfb417f3ee3.efs.ap-southeast-1.amazonaws.com:/ /mnt/efs
```

2. Create a test file:

```
echo "Hello from EFS" | sudo tee /mnt/efs/testfile_efs.txt
```

3. Check the file:

```
ls -l /mnt/efs/testfile_efs.txt

cat /mnt/efs/testfile_efs.txt
```

![](/images/6.clean/8.png)

## 6. Conclusion  
- Successfully deployed **AWS Storage Gateway** connecting On-premises File Server to **AWS S3/EFS**.  
- The system ensures safe, manageable, and monitored data synchronization via **CloudWatch**.
