# Cloudera Tech Assessment
This page outlines and explains the architecture and steps performed for the Tech Assessment for Cloudera. The page will also outline all the reasons of choosing the mentioned architecture and further improvements that could be incorporated.

### Problem Statement
Create a simple web application for serving images that presents a single URL that when opened displays an image (of Candidate's liking).

### Assumptions
1. Entire solution is hosted and created on AWS.
2. <>
3. <>

### Proposed Solution
The proposed solution for the problem statement mentioned above is shown in the architecture below. 

<add image of architecture here>
  
Here are the list of components that were created for the above architecture using Cloudformation and why the below services were leveraged :
1. **VPC - For Creation of secluded resources**
2. **Public Subnets - 2 (Availability Zone A/B)**
3. **Private Subnets - 2 (Availability Zone A/B)**
4. **Launch Configuration - For Creation of EC2 instances (in Private Subnets)**
5. **AutoScaling - For scaling up/down of EC2 Instances**
6. **Security Groups for EC2 instances and Application Load Balancer**
7. **Application Load Balancer - For directing Traffic to one of the EC2 instances**
8. **Target Group - For Application Load Balancer**
9. **Internet Gateway - For patching/software updates required on EC2 instances**
10. **NAT Gateway - For enabling EC2 instances to access the Internet**
11. **IAM Role & IAM Instance Profile - For access to images on S3**






