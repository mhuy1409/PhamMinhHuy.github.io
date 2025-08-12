---
title : "Mount File Share trên máy on-premises và kiểm thử đồng bộ"
date :  "2025-08-12T00:00:00+07:00"
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
### Mount File Share
1. Tạo thư mục mount trên máy Linux:

```
sudo mkdir -p /mnt/workshop
```
2. **Mount NFS** share từ **AWS Storage Gateway**:


```
sudo mount -t nfs 10.0.2.129:/workshop-s3-gateway /mnt/workshop
```


*Thay Gateway-IP bằng địa chỉ IP private của gateway.*

3. Kiểm tra mount có thành công hay không:

```
df -h /mnt/workshop
```

*Kết quả hiển thị filesystem và dung lượng cho thấy mount đã thành công.*

![](/images/5.fwd/1.png)

4.	Tạo file thử nghiệm trên thư mục mount:

```
sudo touch /mnt/workshop/testfile.txt
sudo ls -l /mnt/workshop/
```

File `testfile.txt` sẽ được tạo và hiển thị trong thư mục chia sẻ.

![](/images/5.fwd/2.png)

5.	Kiểm tra file trên **Amazon S3 bucket** backend:

+ Vào **AWS Console** → **S3** → Mở bucket **workshop-s3-gateway**.

+ Kiểm tra file `testfile.txt` đã được đồng bộ lên **S3** chưa.

![](/images/5.fwd/3.png)


### Giám sát Storage Gateway bằng CloudWatch
**Bước 1** – Truy cập **Metrics**

Vào **AWS Console** → **CloudWatch** → **All metrics**.

![](/images/5.fwd/6.png)

Chọn namespace **AWS/StorageGateway**.

**Bước 2**– Tạo **Alarm** giám sát **CachePercentUsed**

Chọn metric **CachePercentUsed** → **Select metric** → **Create alarm**.

![](/images/5.fwd/4.png)

**Điều kiện:**

+ **Threshold type** chọn **Static**

+ **Whenever** chọn **Greater than**

+ **Threshold value** chọn **80**

![](/images/5.fwd/5.png)

**Configure actions:**

1.	**Alarm state trigger**: Để mặc định là **In alarm**.

2.	Send a notification to the following SNS topic:

+ Nếu bạn đã có **SNS topic** chọn từ **Select an existing SNS topic**.

+ Nếu chưa có, chọn **Create new topic** để tạo topic mới.

+ Nhập tên ``StorageGatewayAlerts``.

+ Nhập email để nhận thông báo.

Sau khi tạo hoặc chọn xong, nhớ xác nhận đăng ký email (AWS sẽ gửi email yêu cầu bạn click link xác nhận).




**Bước 3** – Tạo **Alarm** giám sát **FilesFailingUpload**

1. Mở Amazon CloudWatch → Chọn Alarms → Create Alarm.

2. Chọn Select metric → Chọn namespace StorageGateway → File Share Metrics.

3. Chọn **FilesFailingUpload** với ShareId tương ứng.


4. Nhấn **Select metric**

![](/images/5.fwd/8.png)

5. Thiết lập điều kiện alarm:

+ **Threshold type** chọn **Static**

+ Whenever **FilesFailingUpload** is *Greater* than **0**.

![](/images/5.fwd/9.png)

6. Nhấn **Next** → Cấu hình hành động cảnh báo (chọn SNS topic để nhận thông báo qua email hoặc SMS).

![](/images/5.fwd/10.png)

7. Đặt tên alarm ``StorageGateway_FilesFailingUpload_Alarm``.

8. Xem lại và chọn **Create alarm**.
