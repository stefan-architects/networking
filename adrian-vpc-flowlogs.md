## 1. 📖 Adrian - VPC Flow Logs Hands On
Hands‑on exploration of AWS networking fundamentals using a custom Virtual Private Cloud (VPC). This lab helps you understand how traffic moves inside AWS and how to monitor it using VPC Flow Logs.

## 📌 Project Overview
This repository documents my hands‑on practice while learning VPC Flow Logs. I'll be launching EC2 instances to capture, inspect, and troubleshoot network traffic, using IAM roles and permissions to work with VPC Flow Logs and the VPC. Each lesson will be provided separately to clearly show the progression of concepts and exercises.

### 📺 Sources
[Mini Project - Learn how to use VPC Flow logs to diagnose network issues](https://www.youtube.com/watch?v=4HvwQ1uoWEA)

## 2. 🌩️ Skill Building
* Inspect subnets, route tables, and gateways
* Practice CLI networking commands  
* Observe network traffic patterns
* Review accepted vs. rejected traffic  
* Security Group or Network ACL issues
* Interpreting policy structure, including statements, actions, and resources

## 3. 🛰️ AWS Resources & Services
* EC2, S3, IAM, VPC, Cloudwatch
* Sample Python / Node.js apps depending on the lesson
* AWS Console + AWS CLI

## 4. 🔐 IAM Configuration
* EC2 Instance Role:
    * Attached **AmazonSSMManagedInstanceCore** to EC2 instances to establish management sessions rather than requiring SSH keys or long-lived AWS credentials.

* VPC Flow Logs Role:
    * Custom trust policy using **CloudWatchLogsFullAccess** to allow VPC Flow Logs full access to publish log data to Amazon CloudWatch Logs.

## 4. 📟 Flow Logs Triggered by Activity
* **srcaddr / dstaddr** — source and destination IPs  
* **srcport / dstport** — ports used  
* **protocol** — TCP, UDP, ICMP  
* **action** — ACCEPT or REJECT  
* **bytes** — amount of data transferred  
* **packets** — number of packets  
* **log-status** — OK or NODATA 

## 6. 👀 Metrics & Patterns Observed  
* Accepted traffic for normal EC2 operations  
* Rejected traffic when NACLs or security groups block requests  
* Internal VPC communication between private subnets  
* Outbound internet traffic from public subnets  
 
## 7. 👁️ Observations & Next Actions  
### 🏢 *Workplace Applications*
* Review Flow Logs with the team to confirm network behavior  
* Validate whether security rules match intended architecture  
* Identify misconfigurations (wrong routes, blocked ports, etc.)  
* Use logs to troubleshoot connectivity issues
* Build a dashboard for network traffic
* Blocking ICMP with a NACL in the same subnet will allow ICMP traffic
* Blocking ICMP with a NACL in a different subnet will deny ICMP traffic

### 🧙🏽 *Ongoing Development*  
* Integrate CloudWatch Metrics or Alarms for network monitoring  
* Explore VPC Traffic Mirroring for deeper packet inspection
* Create/Revise filters ........*Why*
* Create/Revise CloudWatch alarms ..........*Why*