---
title : "PhamMinhHuy"
date :  "2025-08-12T00:00:00+07:00"
weight : 1 
chapter : false
---
# File Server Migration với Storage Gateway và EFS

### Tổng quan

Trong bài lab này, chúng ta sẽ thực hiện di chuyển dữ liệu từ hệ thống file server truyền thống (on-premises) lên nền tảng đám mây AWS bằng cách sử dụng **AWS Storage Gateway** kết hợp với **Amazon EFS** và **Amazon S3**. Việc này giúp tận dụng ưu điểm của đám mây như khả năng mở rộng linh hoạt, bảo mật cao và dễ dàng quản lý dữ liệu.

Bạn sẽ học cách:

- Triển khai và cấu hình **AWS Storage Gateway** dưới dạng File Gateway.
- Tạo và cấu hình **Amazon EFS** để lưu trữ dữ liệu file system dạng mạng.
- Kết nối máy chủ on-premises hoặc EC2 với Storage Gateway qua giao thức NFS/SMB.
- Đồng bộ dữ liệu tự động giữa on-premises và AWS S3/EFS.
- Kiểm thử và giám sát quá trình đồng bộ dữ liệu.

### Mục tiêu bài lab

- Hiểu rõ kiến trúc và cách hoạt động của Storage Gateway và EFS.
- Thực hành cấu hình môi trường AWS phù hợp cho file server migration.
- Đảm bảo dữ liệu được đồng bộ an toàn và hiệu quả từ on-premises lên đám mây.
- Áp dụng các kỹ thuật giám sát và quản lý dữ liệu sử dụng CloudWatch.

### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Chuẩn bị môi trường Lab](2-Prerequiste/)
 3. [Tạo AWS Storage Gateway](3-Accessibilitytoinstance/)
 4. [Tạo Amazon EFS và S3](4-s3log/)
 5. [Mount File Share trên máy on-premises và kiểm thử đồng bộ](5-Portfwd/)
 6. [Kiểm thử](6-cleanup/)
 7. [Dọn dẹp tài nguyên](7-cleanup/)
