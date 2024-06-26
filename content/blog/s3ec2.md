---
title: Mounting an S3 bucket on an EC2 instance 
date: 2024-02-06T01:25:25.364Z
tags: [AWS]
description: Steps to mount an S3 bucket on an EC2 instance.
---

For use cases such as log collection and analysis, data backup & archiving, and file sharing and collaboration, an S3 bucket can be mounted on an EC2 instance. The procedure makes use of S3FS tool that enables mounting an S3 bucket as a local file system on an EC2 instance running Linux. The steps described below show how to mount an S3 bucket on EC2 instance.

#### Prerequisites:

1. Access to the EC2 Linux instance on which an S3 bucket needs to be mounted.
2. Connectivity between the EC2 instance and S3.
3. Connectivity to GitHub to download the S3FS code onto an EC2 instance.
4. An EC2 IAM role with S3 read and write permissions to read and write files from S3.

#### Steps:

1. Update the system with the following command or using a command applicable to the OS of the EC2 instance.

    ` sudo yum update`

2. Install the S3FS tool which is required to mount an S3 bucket onto an EC2 instance:

   `$ sudo yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel`

3. Next, download the S3FS code from GitHub. Ensure that the EC2 instance has network connectivity to download the code from GitHub as described in the third bullet of prerequisites.

    `$ git clone https://github.com/s3fs-fuse/s3fs-fuse.git`

***Note - s3fs-fuse is a third party tool. Hence, test the steps in a test environment first. The blog writer holds no responsibility of any undesired outcomes and issues.***

4. Once the code is downloaded from GitHub, compile and install it on the EC2 instance.

   ```
   $ cd s3fs-fuse
   $ ./autogen.sh
   $ ./configure --prefix=/usr --with-openssl
   $ make
   $ sudo make install
   ```
5. Once the above commands are run, check S3FS is successfully installed on the instance.

   `$ which s3fs`

6. As described in the second bullet of prerequisites, check the IAM role associated with the instance has read and write permissions to an S3 bucket. The policy with the name "AmazonS3FullAccess" can be used to give full access to S3.

7. Once the required EC2 IAM role is created with S3 permissions and attached to the EC2 instance, create a mount point and an S3 bucket.

   ```
   $ sudo mkdir /ec2s3dir  --- creating a mount point
   $ aws s3 mb s3://ec2s3bucket --region us-west-2 --- creating an S3 bucket in us-west-2
   ```

8. After creating a mount point and an S3 bucket, create an fstab entry and mount all filesystems described in the fstab file.

   `$ s3fs#<S3_bucket> /<mount_point> fuse _netdev,allow_other,uid=1002,gid=1002,iam_role=<IAM_ROLE>,use_cache=/tmp,url=https://s3.region.amazonaws.com 0 0`

    `$ mount -a -- mounting  all filesystems mentioned in the /etc/fstab file`

***Note - Update the aforementioned s3fs line for fstab entry with the details such as S3 bucket name, mount point, IAM role name, and the region (for e.g: us-west-2) as per your use case.***

9. Confirm the mount point using the `df -hT` command.
10. Read files from and write files to mount point similar to it's done on a Linux system. 
