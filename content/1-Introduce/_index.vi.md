---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
**Amazon Elastic Compute Cloud (EC2)** là một dịch vụ điện toán đám mây của AWS, cung cấp khả năng thay đổi kích thước linh hoạt và dễ dàng triển khai các ứng dụng. EC2 cho phép khởi tạo các máy chủ ảo (còn gọi là instances) để chạy các ứng dụng trên nền tảng đám mây AWS.

**Amazon Virtual Private Cloud (VPC)** là dịch vụ của Amazon Web Services (AWS) cho phép người dùng tạo ra một mạng ảo riêng biệt trong môi trường đám mây AWS. Với VPC, bạn có thể định cấu hình mạng ảo của riêng mình, bao gồm việc phân chia các subnet, thiết lập các bảng định tuyến, và quản lý các cổng vào ra, tất cả đều nằm trong một không gian riêng biệt và an toàn.

Các Tính Năng Chính của Amazon VPC:

- Mạng Riêng Tư: Tạo một mạng ảo với các IP riêng biệt và cấu hình IP riêng cho các tài nguyên trong VPC.
- Phân Chia Mạng: Chia VPC thành các subnet công cộng và riêng tư để phân loại và kiểm soát lưu lượng truy cập.
- Cổng và Định Tuyến: Sử dụng Internet Gateway, NAT Gateway và Route Tables để kiểm soát truy cập vào và ra khỏi VPC.
- Bảo Mật: Quản lý lưu lượng truy cập bằng Security Groups và Network ACLs, và sử dụng VPC Peering để kết nối với các VPC khác hoặc các mạng on-premises.

**Mạng con (Subnet)** là một dải địa chỉ IP trong VPC của bạn. Mạng con được sử dụng để phân chia một mạng lớn thành các phần nhỏ hơn, dễ quản lý hơn và có thể tối ưu hóa hiệu suất cũng như bảo mật. Ngoài ra, mạng con được tạo ra để kết nối với các tài nguyên AWS như EC2, RDS khi bạn khởi tạo. Các subnet có thể kết nối với internet, với các VPC khác hay với trung tâm dữ liệu của bạn và định tuyến lưu lượng truy cập đến và đi thông qua các bảng định tuyến (route table).

**Bảng định tuyến (Route table)** là một cấu trúc dữ liệu trong hệ thống mạng dùng để xác định cách thức lưu lượng dữ liệu được định tuyến đến đích trong mạng. Mỗi tuyến trong bảng định tuyến chỉ định phạm vi địa chỉ IP nơi bạn muốn lưu lượng truy cập đi đến (destination) và điểm trung gian (cổng, giao diện mạng hoặc kết nối) mà lưu lượng dữ liệu sẽ được gửi qua trước khi đến đích (target).

**Internet Gateway (IGW)** là một dịch vụ mạng trong Amazon Web Services (AWS) giúp kết nối các tài nguyên trong VPC (Virtual Private Cloud) của bạn với Internet. Nó hoạt động như một điểm kết nối giữa VPC và Internet, cho phép các tài nguyên trong VPC gửi và nhận lưu lượng từ Internet.

**NAT(Network Address Translation) Gateway** là một dịch vụ biên dịch địa chỉ mạng của AWS được sử dụng để cung cấp khả năng truy cập Internet cho các tài nguyên trong một VPC mà không cần phải cho phép lưu lượng từ Internet trực tiếp đến các tài nguyên đó. NAT Gateway giúp các instance trong mạng con riêng tư (private subnet) có thể gửi lưu lượng ra Internet và nhận phản hồi mà không cần có địa chỉ Public IP.

**Public IP** là địa chỉ IP mà thiết bị hoặc dịch vụ sử dụng để giao tiếp trực tiếp với Internet hoặc với các thiết bị ngoài mạng nội bộ. Địa chỉ này phải là duy nhất trên toàn bộ Internet. **Private IP** là địa chỉ IP được sử dụng trong mạng nội bộ và không thể được truy cập trực tiếp từ Internet. Private IP được sử dụng để giao tiếp giữa các thiết bị trong cùng một mạng nội bộ.

**Security Group** là một tính năng quan trọng của Amazon Web Services (AWS) giúp quản lý và kiểm soát lưu lượng mạng vào và ra từ các tài nguyên như EC2 instances, RDS instances, và các dịch vụ khác trong VPC (Virtual Private Cloud). Security Group có 2 tính năng chính là:

- Stateful Firewall: nếu bạn cho phép một kết nối đến (inbound), thì các phản hồi từ kết nối đó sẽ tự động được phép quay lại bất kể quy tắc outbound và ngược lại.
- Connection Tracking: cho phép Security Groups duy trì thông tin về các kết nối mạng hiện tại. Điều này có nghĩa là khi một kết nối được tạo ra và được phép bởi quy tắc inbound, tất cả các phản hồi từ kết nối đó cũng sẽ được cho phép, ngay cả khi không có quy tắc outbound tương ứng.

**Network Access Control List (NACL)** là một cơ chế bảo mật của AWS được sử dụng để kiểm soát lưu lượng ra vào cho các subnet trong Virtual Private Cloud (VPC). NACL hoạt động ở mức subnet và cung cấp thêm một lớp bảo mật ngoài Security Groups, giúp quản lý và kiểm soát truy cập vào các tài nguyên trong mạng VPC. Đặc điểm của NACL:

- Stateless: mỗi yêu cầu vào hoặc ra đều phải được đánh giá độc lập theo các quy tắc của NACL. Nếu bạn cho phép lưu lượng đi vào, bạn cũng cần tạo một quy tắc để cho phép lưu lượng phản hồi đi ra.
- Khác với SG, các quy tắc của NACL có thể được đặt để cho phép hoặc từ chối lưu lượng cụ thể.

Một ví dụ về việc sử dụng NACL là khi cần chặn một địa chỉ đã và đang kết nối vào instance. Với SG ta có thể gỡ các inbound rule của user đó trong SG, nhưng kết nối giữa user đó và instance vẫn tiếp tục do tính connection tracking của security group. Đối với NACL, ta thêm một rule để từ chối kết nối từ IP của user đó, ngay lập tức user này sẽ mất kết nối với instance. 

**Amazon Relational Database Service (RDS)** là một dịch vụ cơ sở dữ liệu quan hệ được quản lý hoàn toàn bởi AWS. Nó giúp đơn giản hóa việc quản lý cơ sở dữ liệu quan hệ trong môi trường đám mây, cung cấp tính năng mở rộng linh hoạt, bảo mật mạnh mẽ, và khả năng sẵn sàng cao, cho phép bạn tập trung vào phát triển ứng dụng mà không cần lo lắng về quản lý cơ sở dữ liệu phức tạp.



