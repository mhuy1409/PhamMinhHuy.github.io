+++
title = "Kiểm thử"
date = 2021
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

### 1. Kiểm thử Mount NFS của Storage Gateway

1. Nhập đoạn bash này vào SSH.
```
mount | grep /mnt/workshop
```

![](/images/6.clean/1.png)

Điều này nghĩa là:
+ EC2 đã kết nối được tới Storage Gateway qua NFS
+ Bạn có thể thao tác đọc/ghi file trong /mnt/workshop
+ Các thao tác file bạn thực hiện trong thư mục này sẽ đồng bộ với S3 thông qua Storage Gateway

![](/images/6.clean/2.png)

2. Kiểm tra thư mục mount:

```
ls -l /mnt/workshop
```

![](/images/6.clean/3.png)

### 2. Kiểm thử đọc và ghi file từ EC2 lên Storage Gateway

1. Tạo file mới:

```
echo "Hello from EC2" | sudo tee /mnt/workshop/filetest1_from_ec2.txt
```

2. Kiểm tra file vừa tạo:

```
ls -l /mnt/workshop/filetest1_from_ec2.txt

cat /mnt/workshop/filetest1_from_ec2.txt
```

![](/images/6.clean/4.png)

### 3. Kiểm thử đồng bộ dữ liệu Storage Gateway với S3 Bucket

Kiểm tra trong **AWS S3** console bucket **workshop-s3-gateway**, đảm bảo file `filetest1_from_ec2.txt` đã xuất hiện.

![](/images/6.clean/5.png)

### 4. Kiểm thử upload file trực tiếp từ EC2 lên S3 (bằng IAM Role)

1. Tạo file:

```
echo "Hello direct S3 upload" > filetest1_s3.txt
```

2. Upload lên S3:

```
aws s3 cp filetest1_s3.txt s3://workshop-s3-gateway/
```

3. Kiểm tra file đã upload:

```
aws s3 ls s3://workshop-s3-gateway/filetest1_s3.txt
```

![](/images/6.clean/6.png)

### 5. Kiểm thử ghi file từ máy on-premise lên Storage Gateway

1. Tạo file test:

```
echo "Hello from on-prem" > /mnt/workshop/filetest1_from_onprem.txt
```

2. Kiểm tra file này có trên EC2:

```
ls -l /mnt/workshop/filetest1_from_onprem.txt

cat /mnt/workshop/filetest1_from_onprem.txt
```

![](/images/6.clean/7.png)


### 6. Kiểm thử xóa file trên Storage Gateway và đồng bộ lên S3

1. Xóa file trên EC2:

```
sudo rm /mnt/workshop/filetest4.txt
```

2. Kiểm tra trên bucket S3 file này đã bị xóa chưa:

```
aws s3 ls s3://workshop-s3-gateway/filetest4.txt
```

Nếu file không còn thì đúng

### 7. Kiểm thử tạo và truy cập file trên EFS 
1. Mount EFS:

```
sudo mount -t nfs4 -o nfsvers=4.1 fs-09848ebfb417f3ee3.efs.ap-southeast-1.amazonaws.com:/ /mnt/efs
```

2. Tạo file thử nghiệm:

```
echo "Hello from EFS" | sudo tee /mnt/efs/testfile_efs.txt
```

3. Kiểm tra file:

```
ls -l /mnt/efs/testfile_efs.txt

cat /mnt/efs/testfile_efs.txt
```
![](/images/6.clean/8.png)

## 6. Kết luận
- Hoàn thành triển khai **AWS Storage Gateway** kết nối On-premises File Server tới **AWS S3/EFS**.
- Hệ thống đảm bảo dữ liệu được đồng bộ an toàn, dễ quản lý, giám sát qua **CloudWatch**.
