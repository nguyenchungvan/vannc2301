---
title : "Cài đặt Java, MVN và triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---

### Cài đặt Java và MVN

1. Chuyển tài khoản root, cập nhật update.

```
  sudo su
  yum update
```
![Connect](/images/3.connect/06-connect.png)

2. Cài đặt Java 21

```
  curl -fL -o https://corretto.aws/downloads/latest/amazon-corretto-21-x64-linux-jdk.tar.gz
  export JAVA_HOME=/urs/lib/jvm/java-21-amazon-corretto
  java -version
```
![Connect](/images/3.connect/07-connect.png)

3. Cài MVN

```
  sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
  sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
  sudo yum install -y apache-maven
  mvn -v
```

![Connect](/images/3.connect/08-connect.png)

### Tải file project từ máy tính lên EC2 thông qua AWS S3

{{% notice note %}}
Trong bài lab này, project được copy từ S3 Bucket đến EC2 server thông qua Internet Gateway và NAT Gateway, có thể dùng VPC Endpoint tăng tăng cường bảo mật, hiệu suất và chi phí khi kết nối các dịch vụ của AWS.
{{% /notice %}}

{{% notice note %}}
Để EC2 có thể tải file project từ S3, ta cần gán roles cho EC2 để có thể truy cập vào S3.
{{% /notice %}}

1. Ở trang [giao diện quản trị của dịch vụ EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:).
  + Chọn **Instances**.
  + Chọn **EC2 Server**.
  + Chọn **Action**.
  + Chọn **Security**.
  + Chọn **Modify IAM role**.

  ![Connect](/images/3.connect/09-connect.png)

2. Tạo IAM role
  + Chọn **Create new IAM role**

![Connect](/images/3.connect/10-connect.png)

  + Trong mục **Roles** ở [giao diện Identity and Access Management (IAM)](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles), chọn **Create role**.

 ![Connect](/images/3.connect/11-connect.png)

  + Ở trang tiếp theo chọn **Trusted entity type** là **AWS service**, mục **Service or use case** chọn **EC2**.

  ![Connect](/images/3.connect/12-connect.png)

  + Bước tiếp theo, chọn quyền **AmazonS3FullAccess** cho EC2, chọn **Next**.

    ![Connect](/images/3.connect/13-connect.png)

  + Điền tên **Role name**, **Description**, và review lại role đã tạo, sau đó chọn **Create role**.

    ![Connect](/images/3.connect/14-connect.png)

    ![Connect](/images/3.connect/15-connect.png)

3. Gán quyền truy cập S3 cho EC2
  + Quay về trang ở **bước 1**, refresh để tải lại các roles.
  + Chọn role **EC2FullAccessS3**.
  + Chọn **Update IAM role**.

    ![Connect](/images/3.connect/16-connect.png)
 ![Connect](/images/3.connect/17-connect.png)

4. Sao chép project lên server
  ```
  aws s3 cp s3://van-bucket-01/My-Phone.zip /ssm-user
```
{{% notice note %}}
Nếu EC2 chưa được gán quyền truy cập S3 sẽ xuất hiện lỗi **fatal error: Unable to locate credentials**.
{{% /notice %}}

 ![Connect](/images/3.connect/18-connect.png)

### Triển khai ứng dụng lên EC2

1. Giải nén tệp
```
  unzip myphone
```
 ![Connect](/images/3.connect/19-connect.png)

2. Cấu hình lại file kết nối với database
  + Truy cập vào file cấu hình của dự án
```
  nano application.properties
```
  + Sửa lại **url**, **username**, **password** ứng với RDS đã tạo, sau đó lưu lại file.

 ![Connect](/images/3.connect/22-connect.png) 

3. Chạy project

```
  mvn spring-boot: run
```

![Connect](/images/3.connect/20-connect.png)

  + Project đã chạy trên EC2 thành công.

![Connect](/images/3.connect/21-connect.png)

4. Tạo Application Load Balancer
+ Ở trang [giao diện quản trị của dịch vụ EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:), chọn **Load Balancers**.
+ Chọn **Create load balancer**.

![Connect](/images/3.connect/23-connect.png)

+ Chọn **Create** Application Load Balancer.

![Connect](/images/3.connect/24-connect.png)

+ Điền tên ALB, chọn Scheme **Internet-facing** để có thể kết nối đến trang web đã chạy, chọn Load banlancer IP address type **IPv4**.

![Connect](/images/3.connect/25-connect.png)

+ Phần **Network mapping**, chọn VPC đã tạo và 2 public subnet ở 2 AZ bên trong VPC để kết nối với ALB.

![Connect](/images/3.connect/26-connect.png)

+ Chọn **Security group** đã tạo cho ALB.

![Connect](/images/3.connect/27-connect.png)

+ Trong phần **Listeners and routing**, chọn **Create target group** để tạo Target group cho ALB.

![Connect](/images/3.connect/28-connect.png)

+ Chọn loại target **Instance** và điền tên **Target group name**.

![Connect](/images/3.connect/29-connect.png)

+ Chọn **Protocal:Port**, **IP address type**, **Heal check**, sau đó chọn **Next**

![Connect](/images/3.connect/30-connect.png)

+ Thêm instance đang chạy vào target group, sau đó chọn **Create target group**.

![Connect](/images/3.connect/31-connect.png)

![Connect](/images/3.connect/32-connect.png)

+ Quay về trang tạo ALB, refresh lại và chọn target group vừa tạo.

![Connect](/images/3.connect/33-connect.png)

+ Xem lại các lựa chọn lần nữa và chọn  **Create load balancer**.

![Connect](/images/3.connect/34-connect.png)

+ Truy cập vào trang web từ DNS của ALB

![Connect](/images/3.connect/35-connect.png)

+ Kết quả khi triển khai ứng dụng thành công

![Connect](/images/3.connect/36-connect.png)

5. Restore database từ bản backup
  + Ở giao diện session manager của EC2, cài đặt postgresql-client.

```
  yum install postgresql -y
  pg_restore --version
```
  ![Connect](/images/3.connect/39-connect.png)

  + Tiến hành restore lại database từ fileb mybackup.sql

```
  pg_restore -h <RDS-endpoint> -p <port> -U <username> -d <database> -v <filebackup.sql>
```
{{% notice info %}}
Version của postgresql từ file backup phải trùng với version của postgresql được cài đặt trên EC2.
{{% /notice %}}

  + Sau khi restore, kiểm tra lại trang web.

  ![Connect](/images/3.connect/40-connect.png)

6. Tạo Auto Scaling Group
  + Vào trang [giao diện quản trị của dịch vụ EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:).
  + Chọn **Instances**.
  + Chọn **EC2 Server**.
  + Chọn **Action**.
  + Chọn **Image and templates**.
  + Chọn **Create image**.

![Connect](/images/3.connect/37-connect.png)

  + Điền tên image cần tạo và mô tả.

![Connect](/images/3.connect/38-connect.png)

  + Giữ các cấu hình mặc định, chọn **Create image**.

![Connect](/images/3.connect/41-connect.png)

  + Chuyển sang [giao diện quản trị của dịch vụ EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:), chọn **Auto Scaling Group**, chọn **Create Auto Scaling Group**.

  ![Connect](/images/3.connect/42-connect.png)

  + Điền tên Auto Scaling Group và chọn **Create launch template**.

  ![Connect](/images/3.connect/43-connect.png)

  + Ở giao diện tạo template, điền tên template và mô tả.

   ![Connect](/images/3.connect/44-connect.png)

  + Chọn **Application and OS Images** là AMI vừa tạo ở trên.

    ![Connect](/images/3.connect/45-connect.png)

  + Chọn **Instance type** và **Key pair** mà bạn muốn.

![Connect](/images/3.connect/46-connect.png)

  + Để mặc định ở **Network settings**.

![Connect](/images/3.connect/47-connect.png)

  + Kiểm tra lại các lựa chọn một lần nữa, chọn **Create launch template**.

![Connect](/images/3.connect/48-connect.png)

  + Chuyển sang trang tạo ASG, refresh lại **Launch template**, chọn launch template vừa tạo.
  + Chọn **Next**.

  ![Connect](/images/3.connect/49-connect.png)

  + Ở trang tiếp theo, trong **Network** chọn VPC của bài lab, chọn các 2 private subnet cần tạo EC2 bên trong.

    ![Connect](/images/3.connect/50-connect.png)

  + Trong mục **Load balancing**, Chọn ALB đã tạo, sau đó chọn **Next**.

  ![Connect](/images/3.connect/51-connect.png)

![Connect](/images/3.connect/52-connect.png)

  + Điền số lượng EC2 bạn muốn tạo, theo kiến trúc ta cần 2 EC2 ở 2 AZ khác nhau. Điền số lượng EC2 duy trì tối thiểu, số lượng EC2 triển khai tối đa.

  ![Connect](/images/3.connect/52-connect.png)

  + Tiếp tục chọn **Next** ở các **Step 5** và **Step 6**.
  + Xem lại các cài đặt một lần nữa, chọn **Create Auto Scaling Group**.

  ![Connect](/images/3.connect/54-connect.png)

  + Sau khi tạo xong cần Attach EC2 ban đầu vào ASG.
  + Chọn **Instances**.
  + Chọn **EC2 Server**.
  + Chọn **Actions**.
  + Chọn **Instances settings**.
  + Chọn **Attach to Auto Scaling Group**.

   ![Connect](/images/3.connect/56-connect.png)

  + Chọn ASG vừa tạo.

   ![Connect](/images/3.connect/57-connect.png)

  + Sau khi gán thành công, ở giao diện **Instance**, xóa instance còn thừa.

   ![Connect](/images/3.connect/55-connect.png)