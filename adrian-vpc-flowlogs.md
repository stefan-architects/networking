## 1. 📖 Adrian - VPC Flow Logs Hands On
In this project, I watched the following YouTube video [Mini Project - Learn how to use VPC Flow logs to diagnose network issues](https://www.youtube.com/watch?v=4HvwQ1uoWEA) to diagnose a connectivity issues between two EC2 in the same VPC, using VPC flow logs

## 2. 🛰️ AWS Resources & Services Used
* EC2, S3, IAM, VPC, Cloudwatch
* Sample Python / Node.js apps depending on the lesson
* AWS Console + AWS CLI

## 3. 🔐 IAM Roles & Access Control
### EC2 Instance Role
- AmazonSSMManagedInstanceCore
- Used for SSM sessions instead of SSH keys

### VPC Flow Logs Role
- Trust policy: `vpc-flow-logs.amazonaws.com`
- Permissions: `CreateLogGroup`, `CreateLogStream`, `PutLogEvents`

## How These Work Together
- EC2 uses IAM role for SSM access
- VPC Flow Logs publish to CloudWatch Logs using IAM role
- CloudWatch monitors EC2 + VPC activity

## 4. 🌩️ Skill Building
* Inspect subnets, route tables, and gateways
* Practice CLI networking commands  
* Observe network traffic patterns
* Review accepted vs. rejected traffic  
* Security Group or Network ACL issues
* Interpreting policy structure, including statements, actions, and resources

## 5. 📟 Flow Logs Triggered by Activity
* **srcaddr / dstaddr** — source and destination IPs  
* **srcport / dstport** — ports used  
* **protocol** — TCP, UDP, ICMP  
* **action** — ACCEPT or REJECT  
* **bytes** — amount of data transferred  
* **packets** — number of packets  
* **log-status** — OK or NODATA 

## 6. 👀 Metrics & Patterns Observed  
* Accepted/Rejected traffic with NACLs or security groups
  * Blocking ICMP with a NACL in the same subnet will allow ICMP traffic
  * Blocking ICMP with a NACL in a different subnet will deny ICMP traffic
* Internal VPC communication between private subnets  
* Outbound internet traffic from public subnets

## 7. 👁️ Observations & Next Actions  
### 🏢 *Workplace Applications*
* Review Flow Logs with the team to confirm network behavior  
* Validate whether security rules match intended architecture  
* Identify misconfigurations (wrong routes, blocked ports, etc.)  
* Build a dashboard for network traffic

### 🧙🏽 *Ongoing Development*  
* Integrate or create CloudWatch Metrics or Alarms for network monitoring