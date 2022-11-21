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
- Create NAT Gateway in Public Subnet AZ1
- Create Private Route table AZ1
- Add routes to this route table, the target of this route table should be the NAT Gateway that we just created
- Add subnet associations to the route table we just created. So it connects with the two private subnets that reside in Availability Zone 1.
- Create another NAT gateway in Public Subnet AZ2
- Create Private Route Table AZ2
- Add routes to this route table, the target of this route table should be the **second** NAT Gateway that we just created
- Add subnet associations to the second route table we just created. So it connects with the two private subnets that reside in Availability Zone 2.

