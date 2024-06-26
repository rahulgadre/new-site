---
title: Installing EC2 Instance Connect on a RHEL based EC2 instance
date: 2023-07-01 10:15:27 +07:00
tags: [AWS]
description: Connecting to EC2 instances via SSH using Amazon EC2 Instance Connect Endpoints
---

In this blog, we will explore how to install the EC2 Instance Connect package on a RHEL based EC2 instance. Please note that the steps require either a SCP connection between the RHEL instance and an instance where the required package is downloaded or the root volume of the instance on which the required package is downloaded needs to be attached to the RHEL based instance to copy and install the required package.

Prerequisites:

- A RHEL based EC2 instance along with an Amazon Linux 2 instance running and accessible. Both instances need to be launched in the same  Availability Zone.
- A key or password-based authentication for SCP access between the 2 instances.

Once the above prerequisites are met, access the Amazon Linux 2 instance either via SSH or Session Manager. Next, run the following commands to download the required EC2 Instance Connect packages.

Commands to download EC2 Instance Connect package - 

```
sudo yumdownloader ec2-instance-connect-selinux
sudo yumdownloader ec2-instance-connect
```

If the above yumdownloader command fails, ensure that the yum-utils package is installed. If not, install it with the command ```sudo yum install yum-utils```.

Once the *ec2-instance-connect-selinux* and *ec2-instance-connect* packages are downloaded on the Amazon Linux 2 instance, copy both the packages from the Amazon Linux 2 instance to the RHEL instance either via SCP or by attaching the root volume of the AL2 instance to the RHEL instance. In case of the latter option, refer to the first 9 steps described under "Method 3: Manually edit the file using a rescue instance" in this [link](https://repost.aws/knowledge-center/ec2-linux-emergency-mode) to an AWS document. \
Once the root volume of the AL2 instance is mounted on the RHEL instance, copy the two packages to the home directory of ec2-user or run the following commands for package installation:

```
sudo rpm -ivh ec2-instance-connect-selinux-1.1-19.amzn2023.noarch.rpm
sudo rpm -ivh ec2-instance-connect-1.1-19.amzn2023.noarch.rpm
```

After successfully running the aforementioned commands, confirm the RHEL instance is now accessible via [EC2 Instance Connect](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide//ec2-instance-connect-methods.html#ec2-instance-connect-connecting-console).
