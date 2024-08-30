---
title : "Create RDS"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.2.2 </b> "
---

1. Go to [RDS service management interface](https://ap-southeast-1.console.aws.amazon.com/rds/home?region=ap-southeast-1#databases:)
+ Select **Databases**.
+ Select **Create database**.

![ConnectPrivate](/images/2.prerequisite/17-createec2.png)

2. On the **Step 1** page

+ Select **Standard create**.
+ Select the database type as **PostgreSQL**.

![ConnectPrivate](/images/2.prerequisite/18-createec2.png)

+ Select the PostgreSQL version.
+ Select **Template** as Freetier.

{{% notice note %}}
Multi-AZ deployment options are only enabled in the Dev/Test and Production templates. With **Multi-AZ DB cluster**, there are two redundant DBs that can handle read traffic, providing higher availability and workload distribution. With **Multi-AZ DB Instance**, there is only one redundant DB that does not handle read traffic, and is only used for failover.
{{% /notice %}}

![ConnectPrivate](/images/2.prerequisite/19-createec2.png)

+ In **Settings**, enter your cluster DB name, the master username used to log in to the database.
+ Select **Self managed** to self-manage password authentication, enter the password and repeat the password to create.

{{% notice note %}}
Database cluster identifier is the database instance name, completely different from the database name.
{{% /notice %}}

![ConnectPrivate](/images/2.prerequisite/20-createec2.png)

+ In the **Instance configuration** section, select the default **DB instance class**. You can select memory-optimized or compute-optimized classes depending on the purpose of using the database (Only available in Dev/Test and Production templates).

![ConnectPrivate](/images/2.prerequisite/21-createec2.png)

+ In the **Storage** section, select **Storage type** as gp2.
+ Fill in the **Allocated storage** you need.

![ConnectPrivate](/images/2.prerequisite/22-createec2.png)

+ In the **Connectivity** section, select **Compute resource** from the newly created EC2.

![ConnectPrivate](/images/2.prerequisite/23-createec2.png)

+ Select **Automatic setup** to let AWS automatically create subnets for RDS.
+ Select **Public access** as **No** to configure traffic routing to only allow databases to connect to EC2 in the same VPC. Databases cannot be connected from outside.

![ConnectPrivate](/images/2.prerequisite/24-createec2.png)

+ Fill in **Database name** in the **Additional configuration** section

![ConnectPrivate](/images/2.prerequisite/25-createec2.png)

+ Select the number of days to automatically retain backups **Back up** and **Encrytion** (if any).

![ConnectPrivate](/images/2.prerequisite/26-createec2.png)

+ In the **Maintainance** section, keep the default options.
+ Review your configuration and estimated costs before selecting **Create database**.

{{% notice note %}}
The suggested cost calculation is for reference only and does not include backup storage, IO (if applicable), or data transfer costs.
{{% /notice %}}

![ConnectPrivate](/images/2.prerequisite/27-createec2.png)

It takes some time for AWS to create your database.