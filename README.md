<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** irahimsindhu@gmail.com  
**Email:** irahimsindhu@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that allows you to create and manage a private virtual network within AWS. It is useful because it gives you full control over your network configuration, including IP address ranges, subnets, route tables, and security settings, enabling you to securely deploy and manage AWS resources.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to establish peering connection between 2 VPCs.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the simplicity in guidance.

### This project took me...

This project took me 42 minutes.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will 2 separate VPCs using the resource map.

### Step 2 - Create a Peering Connection

In this step, I will setup a peering connection between both of my VPCs. Peering connections allows private resources in VPCs to communicate with each other without traversing the public internet.

### Step 3 - Update Route Tables

In this step, I will set up a way for the traffice coming from VPC1 to VPC2 and vice cersa. This step is important to ensure that data, resource etc can be shared easily.

### Step 4 - Launch EC2 Instances

In this step, I will launch a dedicated EC2 instance in both of our VPCs.

---

## Multi-VPC Architecture

I started my project by launching 2 VPCs using the resource map. I set up 1 availability zone, 1 public subnet and 0 private subnet for my VPCs.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because we have to make sure that unique and distinct IPs are assigned to both VPCs. If it is not configured, the IPs will conflict with each other.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances because AWS actually manages a key pair for us and we can access our EC2 instance using AWS EC2 Instance Connect.

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is way through which 2 VPCs can communicate, share resources and other information using their IPs without every traversing the resource being shared using the public internet.

VPCs would use peering connections to separate their resources from public internet. Without a peering connection, VPCs will have to send the resources being shared first to the public internet and then to the other VPC. 

The difference between a Requester and an Accepter in a peering connection is that a requester will initiate the peering connection(in this project, VPC 1 is the requester) and an accepter will accept the request and establish the peering connection.(In this project, VPC 2 is the accepter)

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because there still isn't a rule that dictates/guides the traffice from VPC1 to VPC2 and vice versa. Hence, we need to add a new route in the route tables of both VPC1 and VPC2.

My VPCs' new routes have a destination of the IPv4 CIDR block of the other VPC. 
The routes for VPC1 route table is:
- Destination: 10.2.0.0/16
- Target: Peering Connection
- Peering Connection: VPC1 <> VPC2

The routes for VPC2 route table is:
- Destination: 10.1.0.0/16
- Target: Peering Connection
- Peering Connection: VPC1 <> VPC2

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will Use EC2 Instance Connect to connect to your first EC2 instance.

### Step 6 - Connect to EC2 Instance 1

In this step, I will Use EC2 Instance Connect to connect to Instance 1.

### Step 7 - Test VPC Peering

In this step, I will do the following:
- Get Instance 1 to send test messages to Instance 2.
- Solve connection errors until Instance 2 is able to send messages back.

---

## Troubleshooting Instance Connect

EC2 Instance Connect is used to securely connect to an EC2 instance via SSH directly from the AWS Management Console, without needing to manually manage SSH keys on your local machine.

I was stopped from using EC2 Instance Connect as my instance did not have a IPv4 address. So, it resulted in an error.

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static public IP addresses that do not change dynamically. By associating an Elastic IP with my EC2 instance, the public IP and DNS mapping remained consistent, ensuring reliable connectivity even after the instance was stopped and started.

Elastic IP addresses solved the connection error by providing a permanent public IP address for the EC2 instance. Unlike standard public IP addresses, which can change when an instance is stopped and started, an Elastic IP remains the same. This ensured that the connection settings and DNS mappings stayed consistent, allowing reliable access to the instance.

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command "ping" command.

A successful ping test would validate my VPC peering connection because ping command is used to test the if the connection between 2 resources is established or not. If the connection is established, we get response in terms of packets with time, TTL and sequence number.

I had to update my second EC2 instance's security group because it was not allowing the traffice to reach it hence failing the ping command. I added a new rule that allowed the traffic from all ICMP IPv4 address.

![Image](http://learn.nextwork.org/affectionate_olive_majestic_marjoram/uploads/aws-networks-peering_7a29d352)

---

---
