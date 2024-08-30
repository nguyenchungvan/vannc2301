---
title : "Tạo EC2"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 2.2.1 </b> "
---

### Tạo Security Groups (SG) cho ALB và EC2

Trước tiên ta tạo SG cho ALB:

1. Truy cập [giao diện quản trị dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)
  + Chọn **Security Groups**.
  + Chọn **Create security groups**.
  
![ConnectPrivate](/images/2.prerequisite/10-createec2.png)

2. Tại trang **Bước 1**
  + Điền tên security group, mô tả và thông tin VPC cho security group.
  
![ConnectPrivate](/images/2.prerequisite/08-createec2.png)

  + Cấu hình **Inbound rules**: cho phép tất cả kết nối đến ALB.
  + Cấu hình **Outbound rules**: mặc định cho phép kết nối ra ALB.
  + Chọn tạo SG.

![ConnectPrivate](/images/2.prerequisite/09-createec2.png)

Tiếp theo ta tạo SG cho EC2 tương tự ALB:

  + Cấu hình **Inbound rules**: cho phép tất cả kết nối từ ALB đến EC2.
  + Cấu hình **Outbound rules**: mặc định cho phép kết nối ra EC2.
  + Chọn tạo SG.

![ConnectPrivate](/images/2.prerequisite/11-createec2.png)

Tạo EC2 Server:

1. Truy cập [giao diện quản trị dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)
  + Chọn **Instances**.
  + Chọn **Launch instances**.

![ConnectPrivate](/images/2.prerequisite/12-createec2.png)

2. Tại trang **Bước 1**

  + Điền tên EC2 cần tạo.
  + Chọn **Amazon Machine Image** là **Amazon Linux 2 AMI**.
  + Chọn **Instance type** là **t2.micro**.

![ConnectPrivate](/images/2.prerequisite/13-createec2.png)

  + Ở mục **Key pair**, chọn **Create new key pair**.
  + Điền tên, loại (RSA) và định dạng.
  + Lưu key pair ở thư mục project trên máy tính.

![ConnectPrivate](/images/2.prerequisite/14-createec2.png)

  + Chọn keypair vừa tạo.
  + Chọn **Edit** ở mục **Network settings** để cấu hình mạng cho EC2

![ConnectPrivate](/images/2.prerequisite/15-createec2.png)

  + Chọn **VPC** là VPC vừa tạo.
  + Chọn **Subnet** là private subnet 1.
  + Chọn **Auto-assign public IP**: **disable** (do EC2 ở private subnet, chưa Enable auto-assign public IPv4 address)
  + Ở mục **Firewall**, chọn security group vừa tạo ở trên cho EC2.
  + Trong phần **Configure storage**, để mặc định **8** GiB gp2 cho Root volume.
  + Xem lại các cài đặt một lần nữa, chọn **Launch instance** để khởi tạo.

![ConnectPrivate](/images/2.prerequisite/16-createec2.png)
