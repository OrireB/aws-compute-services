# AWS Compute Services

## Overview
This project demonstrates the use of AWS EC2, Load Balancer, and Auto Scaling services to set up a scalable web application. The instance runs an Apache web server that serves static content. The infrastructure automatically scales based on load.

## Steps
1. Created VPC.
2. Created Internet Gateway, attach to VPC.
3. Create Subnet (Public & Private).
4. Create Route Table.
5. Create a Traget Group.
6. Create a Load Balancer.
7. Create a Security Group.
8. Create a Auto Scaling.
9. Launched an EC2 instance with a custom security group.
10. Installed Apache web server on the EC2 instance.
11. Configured an Auto Scaling Group with an Application Load Balancer.

## Configurations
- **Security Group Rules**: SSH (22), HTTP (80)
 {
  "SecurityGroup": {
    "GroupName": "web-server-sg",
    "GroupId": "sgr-01f796921c89e2df0",
    "InboundRules": [
      {
        "Protocol": "TCP",
        "PortRange": "22",
        "Source": "102.89.44.95/32",
        "Description": "SSH access"
      },
      {
        "Protocol": "TCP",
        "PortRange": "80",
        "Source": "0.0.0.0/0",
        "Description": "HTTP access"
      }
    ]
  }
}

- **EC2 Instance Setup**: 
{
  "EC2Instance": {
    "InstanceId": "i-0d53c2e59793ca53d",
    "InstanceType": "t2.micro",
    "AMI": "ami-00a929b66ed6e0de6",
    "SecurityGroup": "web-server-sg",
    "KeyPair": "KEY-PAIR-TESTSSS",
    "PublicIP": "54.224.171.202",
    "PrivateIP": "10.0.1.224",
    "AvailabilityZone": "us-east-1a",
    "State": "running"
  }
}

- **Auto Scaling Group**: 
 {
  "AutoScalingGroup": {
    "Name": "SG-TEST",
    "DesiredCapacity": 2,
    "MinSize": 1,
    "MaxSize": 2
  }
}


- **Web Server**: Apache (httpd)
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd


- **Load Balancer**: Application Load Balancer with HTTP listener.
{
  "LoadBalancer": {
    "Name": "APL-TEST",
    "DNSName": "APL-TEST-1731585684.us-east-1.elb.amazonaws.com",
    "Listener": {
      "Protocol": "HTTP",
      "Port": "80"
    },
    "TargetGroup": {
      "Name": "TARGET-TEST",
      "Port": "80",
      "Protocol": "HTTP"
    }
  }
}


## Challenges Faced.
- Auto Scaling configuration errors (resolved by reviewing target group health checks).

## Architectural Diagram:
- Below is the Architectural Diagram showing the steps:

  ![Architectural Diagram](https://raw.githubusercontent.com/OrireB/aws-compute-services/42475b7f2476381848b1f304b931a8faaa9ecff2/Auto%20Scaling.drawio.png)
  
---
