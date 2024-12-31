![Alt text](/VPC.png) 

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web app on AWS using a robust and scalable infrastructure. The repository includes a reference architecture diagram and deployment scripts for setting up the web application on an EC2 instance.

## Features and Architecture

The static website hosting solution incorporates the following components:

1. **Virtual Private Cloud (VPC)**  
   Configured a VPC with public and private subnets across two Availability Zones to ensure high availability and fault tolerance.

2. **Internet Gateway**  
   Facilitated connectivity between VPC instances and the Internet.

3. **Security Groups**  
   Implemented Security Groups to act as a network firewall, ensuring controlled inbound and outbound traffic.

4. **Multi-AZ Deployment**  
   Leveraged two Availability Zones for reliability and fault tolerance.

5. **Public Subnets**  
   Hosted infrastructure components like the NAT Gateway and Application Load Balancer in Public Subnets.

6. **Private Subnets**  
   Deployed web servers (EC2 instances) in Private Subnets for enhanced security. Instances accessed the Internet via a NAT Gateway.

7. **Application Load Balancer (ALB)**  
   Used ALB to distribute traffic across an Auto Scaling Group of EC2 instances.

8. **Auto Scaling Group (ASG)**  
   Enabled automatic scaling of EC2 instances to handle varying traffic loads while maintaining availability.

9. **Secure Communication**  
   Used AWS Certificate Manager to secure application communication with HTTPS.

10. **Domain and DNS**  
    Registered a domain name and configured a DNS record using Route 53.

11. **Monitoring and Alerts**  
    Configured Amazon Simple Notification Service (SNS) to provide alerts for activities in the Auto Scaling Group.

12. **Source Control**  
    Stored web application files on GitHub for version control and collaboration.

## Prerequisites

- An AWS account with administrative access.
- Domain name registered in Route 53.
- Static website files stored in a GitHub repository.

## Deployment Steps

### AWS Infrastructure Setup

1. **VPC and Subnets**  
   - Create a VPC with Public and Private Subnets across two Availability Zones.
   - Attach an Internet Gateway to the VPC.

2. **Security Groups**  
   - Define security rules for the Application Load Balancer and EC2 instances.

3. **Application Load Balancer and Auto Scaling Group**  
   - Set up an ALB to route traffic to EC2 instances.
   - Configure an ASG for automatic instance management.

4. **NAT Gateway**  
   - Create a NAT Gateway in a Public Subnet for Private Subnet instances to access the Internet.

5. **Certificate Manager**  
   - Secure communication by issuing an SSL/TLS certificate.

6. **Route 53**  
   - Create a hosted zone and DNS records to point to the ALB.

### EC2 Instance Setup

Run the following Bash script on the EC2 instances to install and configure Apache HTTP Server and deploy the static website:

```bash
#!/bin/bash

sudo su
yum update -y
yum install -y httpd
cd /var/www/html
yum install git -y
git clone https://github.com/wschidugam/host-a-static-website-on-aws.git
cp -R host-a-static-website-on-aws/. /var/www/html/
rm -rf host-a-static-website-on-aws
systemctl enable httpd
systemctl start httpd
```

### Notification Setup

- Use SNS to create topics and subscriptions to receive notifications for Auto Scaling Group activities.

## Repository Structure

- **/scripts**: Deployment and configuration scripts.
- **/diagrams**: Architecture diagrams for reference.
- **/webapp**: Static HTML web application files.

## Benefits of the Solution

- **Scalability**: Automatically adjusts to traffic demands using the Auto Scaling Group.
- **Reliability**: Multi-AZ deployment ensures high availability.
- **Security**: Isolated Private Subnets for EC2 instances, HTTPS communication, and robust security group rules.
- **Cost-Efficiency**: Automatically scales resources up or down based on traffic.
- **Ease of Management**: Simplified version control with GitHub and centralized DNS management with Route 53.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

