## 1. 📖 Rajesh - VPC Flow Logs Hands On
Hands‑on exploration of AWS networking fundamentals using a custom Virtual Private Cloud (VPC). This lab helps you understand how traffic moves inside AWS and how to monitor it using VPC Flow Logs.

## 📌 Project Overview
This repository documents my hands‑on practice while learning VPC Flow Logs. I'll be launching EC2 instances to capture, inspect, and troubleshoot network traffic, using IAM roles and permissions to work with VPC Flow Logs and the VPC. Each lesson will be provided separately to clearly show the progression of concepts and exercises.

### 📺 Sources
[AWS VPC Flow Logs EXPLAINED! Capture & Analyze Traffic Like a Pro!](https://www.youtube.com/watch?v=j4ab0R_XPTA)

## 2. 🌩️ Skill Building  
* Explore a VPC  
* Inspect subnets, route tables, and gateways  
* Practice CLI networking commands  
* Observe network traffic patterns using VPC Flow Logs  
* Review accepted vs. rejected traffic  
* Connect EC2 instance inside and generate traffic

## 3. 🛰️ AWS Resources & Services  
* EC2, S3, IAM, VPC, Cloudwatch
* AWS Console + AWS CLI

## 4. 📟 Flow Logs Triggered by Activity  
VPC Flow Logs capture network metadata for traffic entering or leaving network interfaces. Common fields you’ll observe:

* **srcaddr / dstaddr** — source and destination IPs  
* **srcport / dstport** — ports used  
* **protocol** — TCP, UDP, ICMP  
* **action** — ACCEPT or REJECT  
* **bytes** — amount of data transferred  
* **packets** — number of packets  
* **log-status** — OK or NODATA  

Traffic that triggers Flow Logs:

* SSH connections via EC2 Instance Connect  
* Ping/ICMP tests  
* Curl/wget outbound requests  
* Blocked traffic due to security group or NACL rules  
* Internal VPC communication between subnets  

## 5. 🧪 Flow Log Configuration  
Below is the IAM policy required for CloudWatch Logs to store VPC Flow Logs.  
This ensures AWS can create log groups, create log streams, and write flow log events.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "logs:DescribeLogGroups",
        "logs:DescribeLogStreams"
      ],
      "Resource": "*"
    }
  ]
}
```

### 🧩 Why This Policy Matters  
VPC Flow Logs **cannot** write to CloudWatch without these permissions.  
This policy ensures:

* Flow Logs can create their own log group  
* Streams are created automatically  
* Logs are written continuously  
* You can monitor traffic in real time  

## 6. 👀 Metrics & Patterns Observed  
When Flow Logs are active, you’ll notice:

* Accepted traffic for normal EC2 operations  
* Rejected traffic when NACLs or security groups block requests  
* Internal VPC communication between private subnets  
* Outbound internet traffic from public subnets  
* No logs for traffic that bypasses VPC Flow Logs (e.g., AWS-managed services)  

Flow Logs help validate:

* Security group rules  
* NACL behavior  
* Routing correctness  
* Unexpected or suspicious traffic  

## 7. 👁️ Observations & Next Actions  
### 🏢 *Workplace Applications*
* Review Flow Logs with your team to confirm network behavior  
* Validate whether security rules match intended architecture  
* Identify misconfigurations (wrong routes, blocked ports, etc.)  
* Use logs to troubleshoot connectivity issues  

### 🧙🏽 *Ongoing Development*
* Add more subnets and observe new traffic patterns  
* Test blocked traffic intentionally to see REJECT entries  
* Integrate CloudWatch Metrics or Alarms for network monitoring  
* Build a dashboard for network traffic.
* Cloudformation (***not the first one i built either***)
