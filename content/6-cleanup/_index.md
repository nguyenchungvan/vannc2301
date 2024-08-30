+++
title = "Clean up resources"
date = 2024
weight = 6
chapter = false
pre = "<b>4. </b>"
+++

We will proceed with the following steps to delete the resources we created in this lab.

### Deleting ASG
1. Go to [EC2 service management interface](https://console.aws.amazon.com/ec2/v2/home)
+ Select **Auto Scaling Group**.
+ Select **ASGForEC2**.
+ Select **Action**.
+ Select **Delete**, then enter **delete** to confirm.
+ **When deleting an ASG, all instances managed by the ASG are deleted.**

![Clean](/images/6.clean/01-clean.png)

### Deleting ALB
1. Go to [EC2 service management interface](https://console.aws.amazon.com/ec2/v2/home)
+ Select **Load balancer**.
+ Select **ALBForWS1**.
+ Select **Action**.
+ Select **Delete**, then fill in **confirm** to confirm.

![Clean](/images/6.clean/02-clean.png)

### Delete RDS

1. Access the [RDS service management interface](https://console.aws.amazon.com/ec2/v2/home)
+ Select **Databases**.
+ Select **database-1**.
+ Select **Action**.
+ Select **Delete**.

![Clean](/images/6.clean/03-clean.png)

+ Uncheck **Create final snapshot** and **Retain automated backups**, select **I acknoledge ...** to confirm deleting the database.
+ Fill in **delete me**.

![Clean](/images/6.clean/04-clean.png)

### Delete VPC and related components

1. Access the [VPC service management interface](https://console.aws.amazon.com/ec2/v2/home).
2. Delete **NAT gateways**.
+ Select **NAT gateways**.
+ Select each Nat gateway.
+ Select **Action**.
+ Select **Delete**, then enter **delete** to confirm.
+ Do the same with the remaining Nat gateway.

![Clean](/images/6.clean/05-clean.png)

3. Delete Elastic IP addresses
+ Select **Elastic IPs**.
+ Select both Elastic IPs.
+ Select **Action**.
+ Select **Release Elastic IP addresses**, then enter **Release** to confirm.

![Clean](/images/6.clean/06-clean.png)

4. Delete Internet gateway
+ Select **Internet gateway**.
+ Select **WorkShop01-igw**.
+ Select **Detach from VPC**.
+ Select **Detach internet gateway**.

![Clean](/images/6.clean/07-clean.png)

+ Select **Internet gateway**.
+ Select **WorkShop01-igw**.
+ Select **Delete internet gateway**, then enter **delete** to confirm.

![Clean](/images/6.clean/08-clean.png)

5. Delete the connection of routing tables with subnets
+ Select **Route tables**.
+ Select the routing table.
+ Select **Action**.
+ Select **Edit subnet associations**.

![Clean](/images/6.clean/09-clean.png)

+ Uncheck the associated subnets.
+ Select **Save associations**.
+ Do the same with the remaining routing tables.

![Clean](/images/6.clean/10-clean.png)

6. Delete VPC
+ Select **Your VPCs**.
+ Select **WorkShop01-vpc**.
+ Select **Action**.
+ Select **Delete VPC**, then enter delete to confirm.

![Clean](/images/6.clean/11-clean.png)

### Check costs and invoices
1. Access the [Billing and Cost Management interface](https://us-east-1.console.aws.amazon.com/costmanagement/home?region=ap-southeast-1#/home).

![Clean](/images/6.clean/12-clean.png)

2. Check the costs incurred when using services on AWS.

![Clean](/images/6.clean/13-clean.png)