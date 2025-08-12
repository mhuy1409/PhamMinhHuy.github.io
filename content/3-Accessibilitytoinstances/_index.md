---
title: "Create AWS Storage Gateway"
date: "2025-08-12T00:00:00+07:00"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

1. Go to **AWS Storage Gateway → Create gateway**.

![](/images/3.connect/Gateway3.png)

2. Name it: `WS-SG`

   Choose:
   - Gateway type: **Amazon S3 File Gateway**
   - Host platform: **Amazon EC2** or on-premises VM.

![](/images/3.connect/gateway.png)

3. Select the **VPC/Subnet** same as EFS and S3.  
4. Get the **Activation Key** → **Activate Gateway**.

![](/images/3.connect/Gateway2.png)

6. Connect to AWS Gateway connection options:

+ Choose **IP address**.

+ **Endpoint options**: select **Publicly accessible** to allow Storage Gateway to communicate with AWS over the internet.

+ Click **Next** to proceed to the next step.

![](/images/3.connect/Gateway4.png)

7. In the next step, review and select **Activate gateway**.  
8. Step 4: **Configure gateway**

+ For **CloudWatch log group**, select **Create a new log group**.  
+ For **CloudWatch alarms**, select **Create Storage Gateway's recommended alarms**.  
+ Click **Configure**.

![](/images/3.connect/Gateway5.png)
