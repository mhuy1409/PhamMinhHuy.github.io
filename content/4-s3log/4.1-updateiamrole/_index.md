---
title: "Create AMAZON EFS"
date: "2025-08-12T00:00:00+07:00"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

1. Search for and select **EFS** -> **Create file system**

![](/images/4.s3/EFS1.png)

2. Name it `Workshop-EFS`  
+ Select your Workshop VPC: **Workshop-VPC**  
+ Click **Customize**

![](/images/4.s3/EFS2.png)

3. Step 1:  
+ **File system type**: select **Regional**  
+ **Transition into IA**: select **30 days**  
+ **Transition into Archive**: select **None**  
+ **Throughput mode**: select **Bursting**  
+ Click **Next**

![](/images/4.s3/EFS3.png)

Step 2: **Network Access:**  

+ Select VPC: Workshop-VPC  
+ Create Mount Target for **ap-southeast-1a** with corresponding subnet  
+ Attach Security Group allowing port 2049  

![](/images/4.s3/EFS4.png)

Step 3: **File system policy**: keep default and click **Next**

Step 4: **Review and Create**: review settings and click **Create file system**

![](/images/4.s3/EFS5.png)
