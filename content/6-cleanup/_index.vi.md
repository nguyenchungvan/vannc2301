+++
title = "Dọn dẹp tài nguyên  "
date = 2024
weight = 6
chapter = false
pre = "<b>4. </b>"
+++

Chúng ta sẽ tiến hành các bước sau để xóa các tài nguyên chúng ta đã tạo trong bài thực hành này.

### Xóa ASG
1. Truy cập [giao diện quản trị dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)
  + Chọn **Auto Scaling Group**.
  + Chọn **ASGForEC2**. 
  + Chọn **Action**.
  + Chọn **Delete**, sau đó điền **delete** để xác nhận.
  + **Khi xóa ASG, tất cả instances được quản lý bởi ASG đều bị xóa.**

![Clean](/images/6.clean/01-clean.png)

### Xóa ALB
1. Truy cập [giao diện quản trị dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)
  + Chọn **Load balancer**.
  + Chọn **ALBForWS1**. 
  + Chọn **Action**.
  + Chọn **Delete**, sau đó điền **confirm** để xác nhận.

![Clean](/images/6.clean/02-clean.png)

### Xóa RDS
1. Truy cập [giao diện quản trị dịch vụ RDS](https://console.aws.amazon.com/ec2/v2/home)
  + Chọn **Databases**.
  + Chọn **database-1**. 
  + Chọn **Action**.
  + Chọn **Delete**.

![Clean](/images/6.clean/03-clean.png)

  + Bỏ chọn **Create final snapshot** và **Retain automated backups**, chọn **I acknoledge ...** để xác nhận xóa database.
  + Điền **delete me**.

![Clean](/images/6.clean/04-clean.png)

### Xóa VPC và các thành phần liên quan
1. Truy cập [giao diện quản trị dịch vụ VPC](https://console.aws.amazon.com/ec2/v2/home).
2. Xóa **NAT gateways**.
  + Chọn **NAT gateways**.
  + Chọn từng Nat gateway. 
  + Chọn **Action**.
  + Chọn **Delete**, sau đó điền **delete** để xác nhận.
  + Thực hiện tương tự với Nat gateway còn lại.

  ![Clean](/images/6.clean/05-clean.png)

3. Xóa Elastic IP addresses
  + Chọn **Elastic IPs**.
  + Chọn cả 2 Elastic IPs. 
  + Chọn **Action**.
  + Chọn **Release Elastic IP addresses**, sau đó điền **Release** để xác nhận.

  ![Clean](/images/6.clean/06-clean.png)

4. Xóa Internet gateway
  + Chọn **Internet gateway**.
  + Chọn **WorkShop01-igw**. 
  + Chọn **Detach from VPC**.
  + Chọn **Detach internet gateway**.

  ![Clean](/images/6.clean/07-clean.png)

  + Chọn **Internet gateway**.
  + Chọn **WorkShop01-igw**. 
  + Chọn **Delete internet gateway**, sau đó điền **delete** để xác nhận.

  ![Clean](/images/6.clean/08-clean.png)


5. Xóa kết nối của các bảng định tuyến với các subnet
  + Chọn **Route tables**.
  + Chọn bảng định tuyến. 
  + Chọn **Action**.
  + Chọn **Edit subnet associations**.

   ![Clean](/images/6.clean/09-clean.png)

  + Bỏ chọn các subnet liên kết.
  + Chọn **Save associations**.
  + Thực hiện tương tự với các bảng định tuyến còn lại.

   ![Clean](/images/6.clean/10-clean.png)

6. Xóa VPC
  + Chọn **Your VPCs**.
  + Chọn **WorkShop01-vpc**. 
  + Chọn **Action**.
  + Chọn **Delete VPC**, sau đó điền delete để xác nhận.
  
   ![Clean](/images/6.clean/11-clean.png)

### Kiểm tra chi phí và hóa đơn
1. Truy cập [giao diện quản lý Billing and Cost Management](https://us-east-1.console.aws.amazon.com/costmanagement/home?region=ap-southeast-1#/home).

 ![Clean](/images/6.clean/12-clean.png)

2. Kiểm tra chi phí phát sinh khi sử dụng dịch vụ trên AWS.

 ![Clean](/images/6.clean/13-clean.png)
