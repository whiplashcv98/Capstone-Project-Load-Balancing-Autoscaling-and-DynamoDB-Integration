# Capstone-Project-Load-Balancing-Autoscaling-and-DynamoDB-Integration
This repository documents the architecture and implementation of a scalable and resilient cloud application on AWS.
The project is divided into two main components:

Part 1: Autoscaling and Load Balancing

Part 2: DynamoDB Integration with EC2

The first part focuses on ensuring high availability and responsiveness by automatically adjusting the number of EC2 instances with an Application Load Balancer (ALB). The second part demonstrates how to configure an EC2 instance to interact with a DynamoDB database, using IAM roles and the AWS SDK for Python (Boto3) for secure access.

Part 1: Autoscaling and Load Balancing
Project Overview
This section details the setup of an AWS environment that can automatically scale to handle varying traffic loads. It uses a Virtual Private Cloud (VPC), subnets, an Internet Gateway, and a NAT Gateway to create a secure and accessible network infrastructure.

Step-by-Step Implementation
VPC and Subnet Configuration

Create a new VPC with a specified CIDR block (e.g., 10.0.0.0/16).

Create public and private subnets in two or more Availability Zones.

Set up public and private route tables, and associate them with their respective subnets.

Attach an Internet Gateway to the VPC for public access and a NAT Gateway in a public subnet for outbound private access.

Update the public route table to route traffic through the Internet Gateway.

Security Configurations

Create a Security Group for the Load Balancer to allow incoming HTTP/HTTPS traffic from the internet.

Create a Security Group for EC2 Instances to allow traffic only from the Load Balancer.

Launch EC2 Instances

Launch an EC2 instance in a public subnet, install your application, and then create an AMI (Amazon Machine Image) of the configured instance.

Application Load Balancer (ALB) Configuration

Create an Application Load Balancer in the EC2 console.

Configure the ALB to route traffic to the public subnets and register the EC2 instances in a target group.

Set up health checks to monitor the status of the instances.

Auto Scaling Group (ASG) Setup

Create an Auto Scaling Group using the AMI created in the previous step.

Configure the ASG to span multiple Availability Zones.

Set scaling policies based on CloudWatch alarms (e.g., scale out when CPU exceeds 60% and scale in when it falls below 30%).

Define minimum, desired, and maximum instance counts.

Testing and Optimization

Simulate traffic to test the functionality of both load balancing and autoscaling.

Review CloudWatch logs and dashboards to identify and resolve performance bottlenecks.

Part 2: DynamoDB Integration with EC2
Project Overview
This section focuses on securely connecting an EC2 instance to a DynamoDB table. It uses an IAM role to grant the necessary permissions without embedding credentials directly on the instance, a key security best practice.

Step-by-Step Implementation
Set Up a DynamoDB Table

Create a new DynamoDB table named Students.

Set the Partition key as StudentID with a String data type.

Prepare your EC2 Instance

Launch an EC2 instance with Python installed.

Create an IAM Role with the AmazonDynamoDBFullAccess policy.

Attach this IAM role to your EC2 instance.

Verify access by running a simple AWS CLI command like aws dynamodb list-tables.

Install Boto3 on EC2

Use pip3 to install the AWS SDK for Python:

pip3 install boto3 --user
Create and Run the Python Script

Create a Python script named student_logger.py on your EC2 instance.

The script uses the Boto3 library to connect to your DynamoDB table and insert data. Remember to update the region name in the script.

Run the script with the command:

python3 student_logger.py
Verify that the data was successfully inserted by checking your DynamoDB table in the AWS Console.
