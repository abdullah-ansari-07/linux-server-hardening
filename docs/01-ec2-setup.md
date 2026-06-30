AWS EC2 Setup with Ubuntu
# Prerequisites
- AWS Account
- EC2 Service
- Basic understanding of Linux

# Introduction
This section is a walkthrough of the AWS Cloud Service setup where I setup the EC2 environment and get the instance up and running with Ubuntu.

# Objective
To setup the environment for the project.
I chose EC2 as I only needed the computing power from a cloud system.
I also chose Ubuntu as it has a easy-to-use CLI and makes it easier to manage and configure.
 
- Why Cloud?  
AWS Cloud was preferred over a Virtual Machine as VMs take a lot of space and computing power and also needs to be stored in the device whereas Cloud manages the computing power and stores our information in it's service which can be accessed at any given time.


# Background
- EC2  
EC2 (Elastic Compute Cloud) is AWS's virtual server service which provides scalable computing resources in cloud. AWS Cloud Services remove the need for local hardware or virtual machines completely.
I used the EC2 service in the N. Virginia (us-east-1) region. I chose this as it is one of AWS's most widely supported region.

EC2 in itself provides the virtual compute resources, and to run Ubuntu, I chose the Ubuntu AMI from AWS which is the Ubuntu OS also containing the default software.
Ubuntu AMI was chosen for Ubuntu's stability and beginner-friendly administration.
The instance type is what defines the CPU, RAM, storage and other hardware components.
The t3.micro instance type was preferred as my work was very minute and does not require much computation power.
- SSH Key Pair  
An SSH key pair was generated from AWS for the purpose of accessing the EC2 Ubuntu instance from my local device.
The public key is stored in the EC2 instance while the private key is provided to us in a downloadable .pem file which is used for SSH authentication.
- Security Group  
A Security Group is the virtual firewall attached to an EC2 instance and is provided by AWS. It controls the inbound and outbound network traffic.
This is the first network security layer before traffic reaches the OS in the EC2 instance. It also has specific rules and protocols which it follows to determine which ports are accessible.


# Implementation
I launched an instance from the management console of the EC2 service.

I selected the Ubuntu AMI for the Operating System, t3.micro for the instance type, generated a new SSH key pair, configured the initial security group, launched the instance and waited for the AWS health checks to complete.
The remaining launch configuration used the default AWS-recommended settings. 

The SSH Key Generation gave a downloadable .pem file which contains the private key on my local machine. It is used to SSH into the AWS EC2 instance from my local device.

```text
Launch EC2
        ↓
Choose Ubuntu AMI
        ↓
Choose Instance Type
        ↓
Create Key Pair
        ↓
Configure Security Group
        ↓
Launch Instance
```
# AWS Resources Created
- EC2 Instance
- Ubuntu AMI (selected)
- t3.micro Instance type
- SSH Key Pair
- Security Group
- Root EBS Volume
- Public IPv4 address (auto-assigned)

# Verification
AWS provides a verification within the EC2 management console where it runs it's own checks and approves wether it's good to go.
```text
Instance reached running state
        ↓
EC2 status checks passed
        ↓
Public IPv4 address assigned
```
# Lessons Learned
- Why cloud is preferred over local Virtual Machines
- Role of AMI in a virtual server (template to create EC2 instance)
- How and why SSH keys are used for secure remote access
- Importance of the private key (downloadable .pem file and public key challenge)