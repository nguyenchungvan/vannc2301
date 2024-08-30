---
title : "Tạo RDS"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 2.2.2 </b> "
---

1. Truy cập [giao diện quản trị dịch vụ RDS](https://ap-southeast-1.console.aws.amazon.com/rds/home?region=ap-southeast-1#databases:)
  + Chọn **Databases**.
  + Chọn **Create database**.

![ConnectPrivate](/images/2.prerequisite/17-createec2.png)  

2. Tại trang **Bước 1**

  + Chọn **Standard create**.
  + Chọn loại database là **PostgreSQL**.

![ConnectPrivate](/images/2.prerequisite/18-createec2.png)

  + Chọn phiên bản PostgreSQL.
  + Chọn **Template** là Freetier. 
  
  {{% notice note %}}
Các lựa chọn triển khai ở nhiều AZ chỉ được mở ở các template Dev/Test và Production. Với **Multi-AZ DB cluster**, có hai DB dự phòng có khả năng xử lý lưu lượng đọc, cung cấp tính sẵn sàng cao hơn và phân tán tải công việc. Với **Multi-AZ DB Instance**, Chỉ có một DB dự phòng không xử lý lưu lượng đọc, chỉ dùng để chuyển đổi dự phòng. 
{{% /notice %}}

![ConnectPrivate](/images/2.prerequisite/19-createec2.png)

  + Trong mục **Settings**, điền tên DB cluster của bạn, tên master username dùng để đăng nhập database.
  + Chọn **Self managed** để tự quản lý xác thực bằng mật khẩu, điền mật khẩu và nhắc lại mật khẩu cần tạo.

{{% notice note %}}
Database cluster identifier là tên database instance, khác hoàn toàn với tên của database. 
{{% /notice %}}

![ConnectPrivate](/images/2.prerequisite/20-createec2.png)

  + Ở phần **Instance configuration**, chọn **DB instance class** mặc định. Có thể chọn các lớp tối ưu hóa bộ nhớ hoặc tối ưu hóa tính toán tùy thuộc vào mục đích sử dụng database (Chỉ có ở template Dev/Test và Production).

  ![ConnectPrivate](/images/2.prerequisite/21-createec2.png)

  + Ở phần **Storage**, chọn **Storage type** là gp2. 
  + Điền **Allocated storage** cần dùng.

    ![ConnectPrivate](/images/2.prerequisite/22-createec2.png)

  + Ở phần **Connectivity**, chọn **Compute resource** từ EC2 vừa tạo. 

 ![ConnectPrivate](/images/2.prerequisite/23-createec2.png)

  + Chọn **Automatic setup** để AWS tự tạo các subnet cho RDS.
  + Chọn **Public access** là **No** để cấu hình định tuyến lưu lượng chỉ cho phép database kết nối với EC2 trong cùng VPC. Database không thể kết nối từ bên ngoài.

   ![ConnectPrivate](/images/2.prerequisite/24-createec2.png)
  
  + Điền **Database name** trong phần **Addtionnal configuration**

  ![ConnectPrivate](/images/2.prerequisite/25-createec2.png)

  + Chọn số ngày lưu giữ tự động các bản sao lưu **Back up** và **Encrytion** (Nếu có).

  ![ConnectPrivate](/images/2.prerequisite/26-createec2.png)

  + Trong phần **Maintainance** giữ các lựa chọn mặc định.
  + Xem lại cấu hình và chi phí dự tính trước khi chọn **Create database**.

  {{% notice note %}}
Tính toán chi phí gợi ý chỉ mang tính chất tham khảo, không bao gồm chi phí lưu trữ bản sao lưu, IO (nếu có) hoặc truyền dữ liệu.  
{{% /notice %}}

  ![ConnectPrivate](/images/2.prerequisite/27-createec2.png)

  Mất một khoảng thời gian để AWS tạo ra database của bạn.

