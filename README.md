# Deploy-a-WordPress-Website-on-AWS
This is how I deploy my wordpress website on AWS based on tutorials provided by **Azeez Salu**.
### Lecture 1: Build a Three-Tier AWS Network VPC from Scratch
![flow chart1](https://github.com/Nina0917/Deploy-a-WordPress-Website-on-AWS/blob/main/1668984056393.png)
- Create VPC
- Edit DNS hostnames
- Attatch Internet Gateway to VPC
- Create 2 public subnets on 2 Availability Zones
- Enable auto-assign public IPv4 address for both subnets
- Create public route table
- Add routes to the public route table (simply connect the table to the Internet Gateway)
- Add subnet associations to the public route table. So it connects with the two public subnets.
- Create 4 private subnets
- Check main route table (default route table, created automatically). See if the four private subnets are associated with it.

### Lecture 2: Create Nat Gateways
![flow chart2](https://github.com/Nina0917/Deploy-a-WordPress-Website-on-AWS/blob/main/picture2.jpg)
- Create NAT Gateway in Public Subnet AZ1
- Create Private Route table AZ1
- Add routes to this route table, the target of this route table should be the NAT Gateway that we just created
- Add subnet associations to the route table we just created. So it connects with the two private subnets that reside in Availability Zone 1.
- Create another NAT gateway in Public Subnet AZ2
- Create Private Route Table AZ2
- Add routes to this route table, the target of this route table should be the **second** NAT Gateway that we just created
- Add subnet associations to the second route table we just created. So it connects with the two private subnets that reside in Availability Zone 2.

### Lecture 3: Create the Security Groups
- Create ALB Security Group for Application Load Balancer (Port = 80 and 443)
- Create SSH Security Group (Port = 22)
- Create Webserver Security Group (Port = 80 and 443, Source = ALB Security Group. Port = 22, Source = SSH Security Group)
- Create Database Security Group (Port = 3306, Source = Webserver Security Group)
- Create EFS Security Group for EFS File System

[Security group rules for different use cases](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-rules-reference.html)

### Lecture 4: Create the RDS Instance
![flow chart4](https://github.com/Nina0917/Deploy-a-WordPress-Website-on-AWS/blob/main/lec4.png)
- Before creating RDS database, first we need to create DB subnet group.
- Create database instance using RDS. Record your username and password for the database.

### Lecture 5: Create EFS
![flow chart5](https://github.com/Nina0917/Deploy-a-WordPress-Website-on-AWS/blob/main/lec5.png)
- Create an EFS file system
- During the creation step, remember to set Mount targets in two Private Data Subnets. So the webservers will use the mount
targets to  connect to the EFS

### Lecture 6: Install WordPress
![flow chart6](https://github.com/Nina0917/Deploy-a-WordPress-Website-on-AWS/blob/main/lec6.png)
- Launch EC2 instance on Public Subnet AZ1, call it Setup Server. (In the video, the author has created the key pair. If you do not have a key pari yet, you can create one in ppk format. **Don't create the key pair in pem format and converts it to ppk format, that would not work for some reason.**)
- Use PuTTY to connect to your instance using the key pair.
- Use Commands to install WordPress step by step
- Configure the wp-config.php file using your own database information
- Restart the webserver
- Enter the IPv4 address of EC2.You should see the WordDress form.
- Register and login account on WordPress
