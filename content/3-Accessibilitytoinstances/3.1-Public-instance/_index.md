---
title : "Create connect to EC2 server"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

{{% notice note %}}
EC2 is located on a private subnet and cannot be connected in the usual way. In this lab, we use session manager to create a connection to the server.

{{% /notice %}}

### Create a connection to EC2

1. Access the [admin interface of the AWS System Manager service](https://ap-southeast-1.console.aws.amazon.com/systems-manager/home?region=ap-southeast-1).

+ Select **Fleet Manager**.
+ Select **Account management**.
+ Select **Configure Default Host Management Configuration**.

![Connect](/images/3.connect/01-connect.png)

2. On the **Configure Default Host Management Configuration** page.

+ Select **Enable Default Host Management Configuration**.
+ Select **IAM Role** for Systems Manager to be able to manage your EC2.
+ Select **Configure**.

![Connect](/images/3.connect/02-connect.png)

### Create a connection to EC2

1. Access the [EC2 service management interface](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:).
+ Select **Instance**
+ Select the newly created EC2.
+ Select **Connect**.

![Connect](/images/3.connect/03-connect.png)

2. On the **Connect to instance** page.
+ Select **Session Manager**
+ Select **Connect**.

![Connect](/images/3.connect/04-connect.png)

The interface after connection is as shown below.

![Connect](/images/3.connect/05-connect.png)