---
title : "Session Management"
date :  "2025-08-12T00:00:00+07:00"
weight : 1 
chapter : false
---
# File Server Migration with Storage Gateway and EFS

### Overview

In this lab, we will migrate data from a traditional on-premises file server to the AWS cloud platform using **AWS Storage Gateway** combined with **Amazon EFS** and **Amazon S3**. This approach leverages cloud benefits such as flexible scalability, high security, and easy data management.

You will learn how to:

- Deploy and configure **AWS Storage Gateway** as a File Gateway.
- Create and configure **Amazon EFS** to store network file system data.
- Connect on-premises servers or EC2 instances to the Storage Gateway via NFS/SMB protocols.
- Automatically synchronize data between on-premises and AWS S3/EFS.
- Test and monitor the data synchronization process.

### Lab Objectives

- Understand the architecture and operation of Storage Gateway and EFS.
- Practice configuring the AWS environment suitable for file server migration.
- Ensure safe and efficient data synchronization from on-premises to the cloud.
- Apply monitoring and management techniques using CloudWatch.

### Contents

 1. [Introduction](1-introduce/)
 2. [Lab Environment Preparation](2-Prerequiste/)
 3. [Create AWS Storage Gateway](3-Accessibilitytoinstance/)
 4. [Create Amazon EFS and S3](4-s3log/)
 5. [Mount File Share on On-premises Machine and Test Synchronization](5-Portfwd/)
 6. [Testing](6-cleanup/)
 7. [Clean Up Resources](7-cleanup/)
