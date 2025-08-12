---
title: "Mount File Share on On-Premises Machine and Test Synchronization"
date: "2025-08-12T00:00:00+07:00"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

### Mount File Share

1. Create a mount directory on your Linux machine:

```
sudo mkdir -p /mnt/workshop
```

2. **Mount NFS** share from **AWS Storage Gateway**:

```
sudo mount -t nfs 10.0.2.129:/workshop-s3-gateway /mnt/workshop
```

*Replace Gateway-IP with the private IP address of your gateway.*

3. Check if the mount is successful:

```
df -h /mnt/workshop
```

*The output showing the filesystem and size indicates the mount was successful.*

![](/images/5.fwd/1.png)

4. Create a test file in the mount directory:

```
sudo touch /mnt/workshop/testfile.txt

sudo ls -l /mnt/workshop/
```

The file `testfile.txt` will be created and displayed in the shared directory.

![](/images/5.fwd/2.png)

5. Check the file on the **Amazon S3 bucket** backend:

+ Go to **AWS Console** → **S3** → Open the bucket **workshop-s3-gateway**.

+ Verify that the file `testfile.txt` has been synchronized to **S3**.

![](/images/5.fwd/3.png)


### Monitor Storage Gateway with CloudWatch

**Step 1** – Access **Metrics**

Go to **AWS Console** → **CloudWatch** → **All metrics**.

![](/images/5.fwd/6.png)

Select the namespace **AWS/StorageGateway**.

**Step 2** – Create an **Alarm** to monitor **CachePercentUsed**

Select the metric **CachePercentUsed** → **Select metric** → **Create alarm**.

![](/images/5.fwd/4.png)

**Conditions:**

+ **Threshold type:** select **Static**

+ **Whenever:** select **Greater than**

+ **Threshold value:** set to **80**

![](/images/5.fwd/5.png)

**Configure actions:**

1. **Alarm state trigger:** leave default as **In alarm**.

2. Send a notification to the following SNS topic:

+ If you already have an **SNS topic**, select it under **Select an existing SNS topic**.

+ If not, choose **Create new topic** to create one.

+ Enter the name ``StorageGatewayAlerts``.

+ Enter the email address to receive notifications.

After creating or selecting the topic, remember to confirm the email subscription (AWS will send an email requesting you to click a confirmation link).


**Step 3** – Create an **Alarm** to monitor **FilesFailingUpload**

1. Open Amazon CloudWatch → Select Alarms → Create Alarm.

2. Choose Select metric → Choose namespace StorageGateway → File Share Metrics.

3. Select **FilesFailingUpload** with the corresponding ShareId.

4. Click **Select metric**.

![](/images/5.fwd/8.png)

5. Set alarm conditions:

+ **Threshold type:** select **Static**

+ Whenever **FilesFailingUpload** is *Greater* than **0**.

![](/images/5.fwd/9.png)

6. Click **Next** → Configure alarm actions (choose SNS topic to receive notifications via email or SMS).

![](/images/5.fwd/10.png)

7. Name the alarm ``StorageGateway_FilesFailingUpload_Alarm``.

8. Review and click **Create alarm**.
