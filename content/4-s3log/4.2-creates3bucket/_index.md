---
title: "Create S3 Bucket"
date: "2025-08-12T00:00:00+07:00"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

### 1. Create **S3 Bucket**

Go to **AWS Management Console** → **S3** → **Create bucket**.

![](/images/4.s3/S3.png)

**Configuration:**

+ **Bucket name:** ``workshop-s3-gateway``  
(This name must match the Storage Gateway configuration later.)

+ AWS Region: **Asia Pacific (Singapore) ap-southeast-1** (same region as Storage Gateway).

+ **Bucket type:** select **General purpose**.

+ **Object Ownership:** select **Bucket owner enforced (ACLs disabled)**.

+ **Block Public Access:** Enable **Block all public access** (recommended for security).

![](/images/4.s3/S31.png)

+ **Versioning:** select **Disable** (unless you want to keep multiple versions).

+ **Bucket Key:** select **Enable**.

+ Click **Create bucket**.

![](/images/4.s3/S32.png)

### 2. Create File Share

1. Go back to Storage Gateway → select the gateway Workshop-S3-Gateway.

+ Select **WS-SG** then click **Create file share**.

+ **Gateway:** `WS-SG`

+ **Amazon S3 bucket:** select **workshop-s3-gateway**.

+ **Access protocol:** choose **NFS** or **SMB** (for Windows, choose **SMB**).

+ Click **Create file share**.

![](/images/4.s3/S33.png)
