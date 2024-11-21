 # SETTING UP A SCALABLE FILE STORAGE SYSTEM USING AMAZON ELASTIC FILE SYSTEM
  ## AIM
  To set up a scalable file storage system using Amazon Elastic File System (EFS) for two EC2 instances in different availability zones, enabling shared access to data.
## PROBLEM STATEMENT
  This experiment demonstrates how to configure Amazon EFS to provide a shared storage solution for two Linux EC2 instances across different availability zones, enabling easy data sharing. The aim is to ensure both instances can mount and access the EFS file system and validate data consistency across instances.
## ALGORITHM
 ### Steps 1: Create two EC2 instances in different availability zones.
 Go to the EC2 service in the AWS Management Console.
Launch two Linux-based EC2 instances (e.g., Amazon Linux 2) and place them in different availability zones within the same VPC.
Assign each instance a security group that allows NFS access on port 2049.
 ### Steps 2: Set up a security group that allows necessary communication between the instances and EFS.
 Create or configure a security group that allows inbound NFS traffic on port 2049 from the security group of both EC2 instances.
Attach this security group to the EFS file system to permit access from both instances.
 ### Steps 3: Create an EFS file system and mount it to both EC2 instances.
 In the AWS Console, navigate to the EFS service and select Create file system.
Select the same VPC as your EC2 instances and configure mount targets in the availability zones where your instances are located.
Complete the setup and take note of the file system ID (e.g., fs-064645ac116a12816).
 ### Steps 4: Ensure that the EC2 instances can access the file system and share data between them.
Instance 1
SSH into the first EC2 instance.
Switch to superuser
Install the HTTP server and EFS utilities
Mount the EFS file system to the web server's root directory
Navigate to the mounted directory and create a sample file:

Instance 2
SSH into the second EC2 instance.
Switch to superuser
Install the HTTP server and EFS utilities
Mount the EFS file system to the web server's root directory
Navigate to the mounted directory, list files, and view the content of the file created on Instance 1
## COMMANDS
EC2 Instance 1
```
sudo su
yum install httpd -y
yum install -y amazon-efs-utils
mount -t efs -o tls fs-064645ac116a12816:/ /var/www/html
cd /var/www/html
vi file  # Create a file and add some text
```
EC2 Instance 2
```
sudo su
yum install httpd -y
yum install -y amazon-efs-utils
mount -t efs -o tls fs-064645ac116a12816:/ /var/www/html
cd /var/www/html
ls
cat file  # Verify shared access by reading content created in Instance 1
```
### NAME:Manoj Kumar G
### REG NUMBER:212222230078

## OUTPUT
Both EC2 instances showing EFS mounting.
![image](https://github.com/user-attachments/assets/0dc47aef-f84c-49c2-9e6c-769c8ac2a210)

The creation of a file on Instance 1.
![image](https://github.com/user-attachments/assets/63ce0ab7-e40e-444c-88ae-c7a6ff646fe4)

The display of that file’s contents on Instance 2 to verify shared access
![image](https://github.com/user-attachments/assets/96e2c908-3121-453c-bbb9-735cd6edceeb)


## RESULT
Successfully set up a scalable file storage system using Amazon EFS shared between two Linux EC2 instances in different availability zones, enabling consistent data sharing.
 

  


