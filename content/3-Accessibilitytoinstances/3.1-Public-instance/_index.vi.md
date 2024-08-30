---
title : "Tạo Kết nối đến máy chủ EC2"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

{{% notice note %}}
EC2 nằm ở private subnet không thể kết nối bằng cách thông thường, ở bài lab này chúng ta sử dụng session manager để tạo kết nối đến server.
{{% /notice %}}

### Tạo kết nối đến EC2

1. Truy cập vào [giao diện quản trị của dịch vụ AWS System Manager](https://ap-southeast-1.console.aws.amazon.com/systems-manager/home?region=ap-southeast-1).
  + Chọn **Fleet Manager**.
  + Chọn **Account management**.
  + Chọn **Configure Default Host Management Configuration**.

![Connect](/images/3.connect/01-connect.png)

2. Tại trang **Configure Default Host Management Configuration**.
  + Chọn **Enable Default Host Management Configuration**.
  + Chọn **IAM Role** cho Systems Manager để có thể quản lý EC2 của bạn.
  + Chọn **Configure**.

![Connect](/images/3.connect/02-connect.png)

### Tạo kết nối đến EC2

1. Truy cập vào [giao diện quản trị của dịch vụ EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:).
  + Chọn **Instance**
  + Chọn EC2 vừa tạo.
  + Chọn **Connect**.

![Connect](/images/3.connect/03-connect.png)

2. Tại trang **Connect to instance**.
  + Chọn **Session Manager**
  + Chọn **Connect**.

![Connect](/images/3.connect/04-connect.png)

Giao diện sau khi kết nối như hình bên dưới.

![Connect](/images/3.connect/05-connect.png)

