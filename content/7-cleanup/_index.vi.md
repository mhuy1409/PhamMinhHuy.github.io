---
title : "Dọn dẹp tài nguyên"
date :  "2025-08-12T00:00:00+07:00"
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
Hướng dẫn dọn dẹp toàn bộ tài nguyên của workshop này để tránh tốn phí.
Mình sẽ đi theo đúng thứ tự ngược lại so với khi tạo, để không bị lỗi do phụ thuộc giữa các dịch vụ.

### 1. Gỡ bỏ EFS trên các EC2
Trước khi xóa EFS, cần ngắt kết nối trên EC2:

```
sudo umount /mnt/efs
```

Nếu có nhiều EC2 cùng mount, làm trên từng EC2.

### 2. Xóa Amazon EFS
+ Vào **AWS Console** → **EFS**.

+ Chọn file system **Workshop-EFS**.

+ Ấn vào **Delete**:

+ Nhập ID xác nhận xóa

![](/images/6.clean/9.png)

Đợi vài phút để EFS xóa xong.

### 3. Gỡ bỏ Storage Gateway
Vào **AWS Storage Gateway** → **File shares**:

Xóa File Share **workshop-s3-gateway** trước.

![](/images/6.clean/10.png)

Sau đó quay lại **Gateways** → chọn gateway **WS-SG** → **Delete gateway**.

![](/images/6.clean/11.png)

Gỡ bỏ instance EC2 chạy **Storage Gateway** (nếu bạn triển khai bằng EC2):

Vào **EC2**→ **Instances** → chọn **gateway instance** → **Terminate**.

### 4. Xóa S3 bucket
Mở **S3** → Chọn bucket **workshop-s3-gateway**.

Chọn **Empty** (Empty bucket) → Xác nhận bằng cách gõ tên bucket → Bấm **Empty**.

Sau khi trống, quay lại **Bucket list** → Chọn bucket → **Delete** → Gõ tên bucket → **Delete bucket**.

![](/images/6.clean/12.png)

### 5. Xóa EC2
Vào **EC2** → **Instances** → chọn **Workshop-EC2**.

**Terminate**.

![](/images/6.clean/13.png)

Nếu không dùng key pair nữa → vào Key Pairs → xóa key pair vừa tạo.

### 6. Xóa VPC & các thành phần
Vào *EC2* → **Security Groups**:

Xóa security group đã tạo cho workshop.

Vào **VPC** → **Subnets**:

Xóa cả **Public** và **Private subnet**.

![](/images/6.clean/14.png)

Vào **VPC** → **Route tables**:

Xóa route table custom.

![](/images/6.clean/15.png)

Vào **VPC** → **Internet Gateways**:

Detach IGW **Workshop-IGW** khỏi VPC.

![](/images/6.clean/16.png)

Xóa **Workshop-IGW**.

Cuối cùng, xóa VPC **Workshop-VPC**.

![](/images/6.clean/17.png)

### 7. Xóa IAM Role
Vào **IAM** → **Roles**.

Xóa IAM Role bạn đã tạo cho **EC2/Storage Gateway** trong workshop.

**Kết quả:** Sau khi làm hết các bước trên, toàn bộ tài nguyên trong workshop sẽ bị xóa, bạn sẽ không bị tốn phí lưu trữ hay chạy máy chủ nữa.