# Cloudera Tech Assessment

This page outlines and explains the architecture and steps performed for the Tech Assessment for Cloudera. The page will also outline all the reasons of choosing the mentioned architecture and further improvements that could be incorporated.

### Problem Statement

Create a simple web application for serving images that presents a single URL that when opened displays an image (of Candidate's liking).

### Assumptions

1. Entire solution is hosted and created on AWS.
2. Cloudformation is the choice for spinning up all the resources in AWS
3. ALl AWS resources are created in the same VPC

### Proposed Solution

The proposed solution for the problem statement mentioned above is shown in the architecture below. <Add more text here>

![Solution Architecture](/images/Architecture.PNG)
  
#### List of Components Leveraged and Why :

1. *VPC - For Creation of secluded resources*
2. *Public Subnets - 2 (Availability Zone A/B)*
3. *Private Subnets - 2 (Availability Zone A/B) for creating EC2 instances*
4. *Launch Configuration - For Creation of EC2 instances (in Private Subnets)*
5. *AutoScaling - For scaling up/down of EC2 Instances*
6. *Security Groups for EC2 instances and Application Load Balancer*
7. *Application Load Balancer - For directing Traffic to one of the EC2 instances*
8. *Target Group - For Application Load Balancer*
9. *Internet Gateway - For patching/software updates required on EC2 instances*
10. *NAT Gateway - For enabling EC2 instances to access the Internet*
11. *IAM Role & IAM Instance Profile - For access to images on S3*

#### Estimate of Cloud Costs:

The overall costs associated with the Proposed Architecture are for the the below componenents:

1. EC2 Instances created (total 2)
2. NAT Gateway (both Duration & Data sent through NAT Gateway)

Using the *AWS Simple Monthly Calculator* the approximate cost calculated is $18.71 (USD). The cost is primarily for EC2 instances and S3. Since, we are using a NAT Gateway, the duration and Data sent through it will also incur costs (this cannot be captured in the Calculator). Below, is a screenshot of the costs:

![Solution Architecture](/images/Costs.PNG)


#### Scalability

The solution is highly scalable in relation to 3 factors - Storage, Data Availability & Requests. Let's take a look at both these factors:

##### Storage & Data Availability

For Storage and Data availability for the Application, the solution uses AWS S3 which is highly scalable, resilient and provides 99.999999999% (11 9's) durability. By using S3, the architecture promises to meet the business requirements at all times. AWS S3 can scale up/down based on requirements and there is no upfront charges / resource procurement cycles.

#### Performance

In terms of Performance, the architecture handles it in 2 ways : Performance of Storage & Performance of the Application to display images. Since, we have already mentioned about Performance and Scalability of S3, let's talk about the latter. The Performance is handled in 2 ways - Using Autoscaling (in case an EC2 instance goes down) & in terms of Health Checks performed by the Application Load Balancer for EC2 instances. In either cases, the minimum number of EC2 instances configured are 2 (to keep the load balanced). Below, snippets from the Cloudforamation YAML highlight the two scenarios :

![AutoScaling](/images/autoscaling.PNG)

![Health Checks](/images/healthcheck.PNG)


#### Security Considerations

Since Security in an Architecture is of Paramount importance, the following features are implemented in the solution. All the security features make sure that unintended access to the AWS resources in not allowed. 

1. EC2 instances are placed in Private Subnets with no Public IPs
2. No Traffic enters/leaves the VPC
3. The Security Groups for EC2 instances only allow traffic from the Application Load Balancer's Security Group on Port 80
4. The Application Load Balancer can only be accessed on Port 80
5. No ssh allowed on EC2 instances
6. Internet Traffic allowed on EC2 instances only via NAT Gateway
7. Images Stored on S3 can only be accessed via IAM Role
8. Bucket created is Private only
9. No Bastion Host provided which can SSH to EC2 instances


#### Application Provision & Automation

Since, all the resources created for the Solution are automated and created via Cloudformation, its very easy for the entire AWS stack to be recreated and provisioned (say in Region Failure). If we have to share the application for someone else to build and run, all we need to provide is the Cloudforamtion YAML. Since, there are no dependencies for a specific AWS Account/person, the YAML will run on any AWS account in chosen Region.


#### Application Portability

The existing Cloudformation is YAML based and can be easily ported to run on another Cloud provider like Google's Deployment Manager or Azure's Resource Manager <Talk about Terraform>
  
#### Comparison 

#### Enhancements





