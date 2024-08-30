---
title : "Install Java, MVN and deploy application"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---
### Install Java and MVN

1. Switch root account, update.

``` 
sudo su yum update 
``` 

![Connect](/images/3.connect/06-connect.png) 

2. Install Java 21 

``` 
curl -fL -o https://corretto.aws/downloads/latest/amazon-corretto-21-x64-linux-jdk.tar.gz export JAVA_HOME=/urs/lib/jvm/java-21-amazon-corretto java -version 
``` 

![Connect](/images/3.connect/07-connect.png) 

3. Install MVN 
``` 
sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven
mvn -v
```

![Connect](/images/3.connect/08-connect.png)

### Upload project file from computer to EC2 via AWS S3

{{% notice note %}}
In this lab, the project is copied from S3 Bucket to EC2 server via Internet Gateway and NAT Gateway, can use VPC Endpoint to increase security, performance and cost when connecting AWS services.

{{% /notice %}}

{{% notice note %}}
For EC2 to be able to download project file from S3, we need to assign roles to EC2 to be able to access S3.
{{% /notice %}}

1. On the [EC2 service management interface](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:) page.

+ Select **Instances**.
+ Select **EC2 Server**.
+ Select **Action**.
+ Select **Security**.
+ Select **Modify IAM role**.

![Connect](/images/3.connect/09-connect.png) 

2. Create an IAM role 
+ Select **Create new IAM role** 

![Connect](/images/3.connect/10-connect.png) 

+ In the **Roles** section in [Identity and Access Management (IAM) interface](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles), select **Cre ate role**.

 ![Connect](/images/3.connect/11-connect.png) 
 
 + On the next page select **Trusted entity type** as **AWS service**, in **Service or use case** select **EC2**.

 ![Connect](/images/3.connect/12-connect.png) 
 
 + Next step, select **AmazonS3FullAccess** permission for EC2, select **Next**.

 ![Connect](/images/3.connect/13-connect.png)

+ Fill in **Role name**, **Description**, and review the created role, then select **Create role**.

![Connect](/images/3.connect/14-connect.png)

![Connect](/images/3.connect/15-connect.png)

3. Assign S3 access to EC2
+ Return to the page in **step 1**, refresh to reload the roles.
+ Select the role **EC2FullAccessS3**.
+ Select **Update IAM role**.

![Connect](/images/3.connect/16-connect.png)
![Connect](/images/3.connect/17-connect.png)

4. Copy the project to the server
```
aws s3 cp s3://van-bucket-01/My-Phone.zip /ssm-user
```
{{% notice note %}}
If EC2 has not been assigned S3 access rights, an error **fatal error: Unable to locate credentials** will appear.
{{% /notice %}}

![Connect](/images/3.connect/18-connect.png)

### Deploy the application to EC2

1. Unzip the file

```
unzip myphone
```
![Connect](/images/3.connect/19-connect.png)

2. Reconfigure the connection file to the database

+ Access the project configuration file

```
nano application.properties
```
+ Edit **url**, **username**, **password** corresponding to the created RDS, then save the file.

![Connect](/images/3.connect/22-connect.png)

3. Run the project

```
mvn spring-boot: run
```

![Connect](/images/3.connect/20-connect.png)

+ The project has run successfully on EC2.

![Connect](/images/3.connect/21-connect.png)

4. Create Application Load Balancer
+ On the [EC2 service management interface](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:) page, select **Load Balancers**.
+ Select **Create load balancer**.

![Connect](/images/3.connect/23-connect.png)

+ Select **Create** Application Load Balancer.

![Connect](/images/3.connect/24-connect.png)

+ Fill in the ALB name, select Scheme **Internet-facing** to be able to connect to the running website, select Load banlancer IP address type **IPv4**.

![Connect](/images/3.connect/25-connect.png)

+ In the **Network mapping** section, select the created VPC and 2 public subnets in 2 AZs inside the VPC to connect to the ALB.

![Connect](/images/3.connect/26-connect.png)

+ Select the **Security group** created for ALB.

![Connect](/images/3.connect/27-connect.png)

+ In the **Listeners and routing** section, select **Create target group** to create a Target group for ALB.

![Connect](/images/3.connect/28-connect.png)

+ Select the target type **Instance** and enter the **Target group name**.

![Connect](/images/3.connect/29-connect.png)

+ Select **Protocal:Port**, **IP address type**, **Heal check**, then select **Next**

![Connect](/images/3.connect/30-connect.png)

+ Add the running instance to the target group, then select **Create target group**.

![Connect](/images/3.connect/31-connect.png)

![Connect](/images/3.connect/32-connect.png)

+ Return to the ALB creation page, refresh and select the target group you just created.

![Connect](/images/3.connect/33-connect.png)

+ Review the options again and select **Create load balancer**.

![Connect](/images/3.connect/34-connect.png)

+ Access the website from the ALB's DNS

![Connect](/images/3.connect/35-connect.png)

+ Result when the application is successfully deployed

![Connect](/images/3.connect/36-connect.png)

5. Restore database from backup

+ In the EC2 session manager interface, install postgresql-client.

```
yum install postgresql -y
pg_restore --version
```

![Connect](/images/3.connect/39-connect.png)

+ Restore the database from the fileb mybackup.sql

```
pg_restore -h <RDS-endpoint> -p <port> -U <username> -d <database> -v <filebackup.sql>
```

{{% notice info %}}
The version of postgresql from the backup file must match the version of postgresql installed on EC2.

{{% /notice %}}

+ After restoring, check the website again.

![Connect](/images/3.connect/40-connect.png)

6. Create Auto Scaling Group
+ Go to the [EC2 service management interface](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:) page.
+ Select **Instances**.
+ Select **EC2 Server**.
+ Select **Action**.
+ Select **Image and templates**.
+ Select **Create image**.

![Connect](/images/3.connect/37-connect.png)

+ Fill in the image name and description.

![Connect](/images/3.connect/38-connect.png)

+ Keep the default configurations, select **Create image**.

![Connect](/images/3.connect/41-connect.png)

+ Switch to [EC2 service management interface](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Home:), select **Auto Scaling Group**, select **Create Auto Scaling Group**.

![Connect](/images/3.connect/42-connect.png)

+ Fill in the Auto Scaling Group name and select **Create launch template**.

![Connect](/images/3.connect/43-connect.png)

+ In the template creation interface, fill in the template name and description.

![Connect](/images/3.connect/44-connect.png)

+ Select **Application and OS Images** which is the AMI created above.

![Connect](/images/3.connect/45-connect.png)

+ Select the **Instance type** and **Key pair** you want.

![Connect](/images/3.connect/46-connect.png)

+ Leave the default in **Network settings**.

![Connect](/images/3.connect/47-connect.png)

+ Check the options again, select **Create launch template**.

![Connect](/images/3.connect/48-connect.png)

+ Go to the ASG creation page, refresh the **Launch template**, select the launch template you just created.

+ Select **Next**.

![Connect](/images/3.connect/49-connect.png)

+ On the next page, in **Network** select the lab's VPC, select the 2 private subnets you need to create EC2 inside.

![Connect](/images/3.connect/50-connect.png)

+ In the **Load balancing** section, select the created ALB, then select **Next**.

![Connect](/images/3.connect/51-connect.png)

![Connect](/images/3.connect/52-connect.png)

+ Fill in the number of EC2s you want to create, according to the architecture we need 2 EC2s in 2 different AZs. Fill in the minimum number of EC2s to maintain, the maximum number of EC2s to deploy.

![Connect](/images/3.connect/52-connect.png)

+ Continue to select **Next** in **Step 5** and **Step 6**.
+ Review the settings again, select **Create Auto Scaling Group**.

![Connect](/images/3.connect/54-connect.png)

+ After creating, you need to Attach the original EC2 to ASG.
+ Select **Instances**.
+ Select **EC2 Server**.
+ Select **Actions**.
+ Select **Instances settings**.
+ Select **Attach to Auto Scaling Group**.

![Connect](/images/3.connect/56-connect.png)

+ Select the newly created ASG.

![Connect](/images/3.connect/57-connect.png)

+ After successfully assigning, in the **Instance** interface, delete the remaining instance.

![Connect](/images/3.connect/55-connect.png)