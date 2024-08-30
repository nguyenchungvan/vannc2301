---
title : "Create EC2 instance"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.2.1 </b> "
---

### Create Security Groups (SG) for ALB and EC2

First, we create SG for ALB:

1. Access [EC2 service management interface](https://console.aws.amazon.com/ec2/v2/home)
+ Select **Security Groups**.
+ Select **Create security groups**.

![ConnectPrivate](/images/2.prerequisite/10-createec2.png)

2. On the **Step 1** page
+ Fill in the security group name, description and VPC information for the security group.

![ConnectPrivate](/images/2.prerequisite/08-createec2.png)

+ Configure **Inbound rules**: allow all connections to ALB.
+ Configure **Outbound rules**: allow connections out of ALB by default.
+ Select create SG.

![ConnectPrivate](/images/2.prerequisite/09-createec2.png)

Next, we create SG for EC2 similar to ALB:

+ Configure **Inbound rules**: allow all connections from ALB to EC2.
+ Configure **Outbound rules**: allow connections to EC2 by default.
+ Select to create SG.

![ConnectPrivate](/images/2.prerequisite/11-createec2.png)

Create EC2 Server:

1. Access [EC2 service management interface](https://console.aws.amazon.com/ec2/v2/home)
+ Select **Instances**.
+ Select **Launch instances**.

![ConnectPrivate](/images/2.prerequisite/12-createec2.png)

2. On the **Step 1** page
+ Enter the name of the EC2 to create.
+ Select **Amazon Machine Image** as **Amazon Linux 2 AMI**
+ Select **Instance type** as **t2.micro**.

![ConnectPrivate](/images/2.prerequisite/13-createec2.png)

+ In the **Key pair** section, select **Create new key pair**.
+ Fill in the name, type (RSA) and format.
+ Save the key pair in the project folder on your computer.

![ConnectPrivate](/images/2.prerequisite/14-createec2.png)

+ Select the newly created keypair.
+ Select **Edit** in the **Network settings** section to configure the network for EC2

![ConnectPrivate](/images/2.prerequisite/15-createec2.png)

+ Select **VPC** as the newly created VPC.
+ Select **Subnet** as private subnet 1.
+ Select **Auto-assign public IP**: **disable** (because EC2 is in private subnet, auto-assign public IPv4 address has not been enabled)
+ In **Firewall**, select the security group just created above for EC2.
+ In **Configure storage**, leave the default **8** GiB gp2 for Root volume.
+ Review the settings again, select **Launch instance** to initialize.

![ConnectPrivate](/images/2.prerequisite/16-createec2.png)