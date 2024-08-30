---
title : "Chuẩn bị VPC"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---


Trong bước này, chúng ta sẽ cần tạo một kiến trúc mạng VPC có 2 public subnet, 2 private subnet, internet gateway và NAT gatway.

Tổng quan kiến trúc sau khi các bạn hoàn tất bước này sẽ như sau:

![VPC](/images/log.png)


### Tạo VPC

1. Truy cập vào [giao diện quản trị dịch vụ VPC](https://ap-southeast-1.console.aws.amazon.com/vpcconsole/home?region=ap-southeast-1#Home:)
+ Chọn **Your VPCs**. 
+ Chọn **Create VPC**.

![ConnectPrivate](/images/2.prerequisite/01-createvpc.png)

2. Tại trang **Bước 1**.
+ Chọn **VPC and more** để tạo nhanh kiến trúc VPC theo yêu cầu.
+ Điền tên VPC và dải IPv4 mà bạn muốn tạo

![ConnectPrivate](/images/2.prerequisite/02-createvpc.png)

+ Ở mục **Number of Availability Zones (AZs)** chọn 2 AZs.
+ Ở mục **Number of public subnets** chọn **2** subnets.
+ Ở mục **Number of private subnets** chọn **2** subnets.
+ Ở mục **NAT gateways** chọn **1 per AZ**.
+ Ở mục **VPC endpoints** chọn **None**.

![ConnectPrivate](/images/2.prerequisite/03-createvpc.png)

+ Xem lại các lựa chọn và xác nhận tạo VPC **Create VPC**.

![ConnectPrivate](/images/2.prerequisite/04-createvpc.png)

3. Sau khi VPC được tạo xong, kiểm tra các thành phần bên trong VPC như subnet hay các bảng định tuyến có đúng yêu cầu.

![ConnectPrivate](/images/2.prerequisite/05-createvpc.png)

+ Bảng định tuyến của **public subnet**: định tuyến lưu lượng trong VPC và ra ngoài qua internet gateway, dùng chung cho cả 2 public subnet.

![ConnectPrivate](/images/2.prerequisite/06-createvpc.png)

+ Bảng định tuyến của **private subnet**: định tuyến lưu lượng trong VPC và ra ngoài qua NAT gateway, mỗi bảng định tuyến được sử dụng cho mỗi private subnet và NAT gateway ứng với subnet đó.

![ConnectPrivate](/images/2.prerequisite/07-createvpc.png)


