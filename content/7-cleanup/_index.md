---
title: "Clean Up Resources"
date: "2025-08-12T00:00:00+07:00"
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

Instructions to clean up all resources from this workshop to avoid incurring charges.  
I will follow the reverse order of creation to avoid errors due to dependencies between services.

### 1. Unmount EFS on EC2 Instances  
Before deleting EFS, unmount it on EC2 instances:

```
sudo umount /mnt/efs
```

If multiple EC2s have the mount, do this on each EC2.

### 2. Delete Amazon EFS  
+ Go to AWS Console → EFS.  
+ Select the file system Workshop-EFS.  
+ Click **Delete**:  
+ Enter the ID to confirm deletion.

![](/images/6.clean/9.png)

Wait a few minutes for EFS to be deleted.

### 3. Remove Storage Gateway  
Go to AWS Storage Gateway → File shares:  

Delete the file share `workshop-s3-gateway` first.

![](/images/6.clean/10.png)

Then go back to Gateways → select gateway `WS-SG` → Delete gateway.

![](/images/6.clean/11.png)

Terminate the EC2 instance running Storage Gateway (if deployed via EC2):  
Go to EC2 → Instances → select the gateway instance → Terminate.

### 4. Delete S3 Bucket  
Open S3 → Select bucket `workshop-s3-gateway`.  

Choose **Empty (Empty bucket)** → Confirm by typing the bucket name → Click **Empty**.

After emptying, return to Bucket list → Select bucket → Delete → Type bucket name → Delete bucket.

![](/images/6.clean/12.png)

### 5. Delete EC2  
Go to EC2 → Instances → select `Workshop-EC2`.  

Terminate the instance.

![](/images/6.clean/13.png)

If you no longer need the key pair → go to Key Pairs → delete the created key pair.

### 6. Delete VPC & Related Components  
Go to EC2 → Security Groups:  

Delete the security groups created for the workshop.

Go to VPC → Subnets:  

Delete both Public and Private subnets.

![](/images/6.clean/14.png)

Go to VPC → Route Tables:  

Delete the custom route table.

![](/images/6.clean/15.png)

Go to VPC → Internet Gateways:  

Detach the IGW `Workshop-IGW` from the VPC.

![](/images/6.clean/16.png)

Delete `Workshop-IGW`.

Finally, delete the VPC `Workshop-VPC`.

![](/images/6.clean/17.png)

### 7. Delete IAM Role  
Go to IAM → Roles.

Delete the IAM Role you created for EC2/Storage Gateway in this workshop.

---

Result: After completing all the above steps, all resources from the workshop will be deleted, and you will no longer incur storage or compute charges.
