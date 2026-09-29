# VPC Set-up
- [Building a Secure and Scalable Three-Tier Architecture on AWS using CloudFormation](https://repost.aws/articles/ARGpERJ3jISbOAlnmfVUsvMQ/building-a-secure-and-scalable-three-tier-architecture-on-aws-using-cloudformation)

## 🌐 **1. Presentation Tier (Web Tier)**  
**Purpose:** Handle all user‑facing traffic and route requests into the application.

### **Key Components**
- **Application Load Balancer (ALB)**  
  - Placed in **public subnets** so it can receive traffic directly from the internet.  
  - Terminates HTTPS, performs routing, health checks, and supports WAF if needed.

- **ChaosPublicSubnets**  
  - Public subnets with an Internet Gateway route.  
  - Host only internet‑facing resources (ALB, bastion if used).  
  - No application or database workloads here.

### **Why this matters**
- Ensures external traffic never directly touches your application servers.  
- Provides a clean separation between public and private resources.

---

## ⚙️ **2. Application Tier (App Tier)**  
**Purpose:** Run business logic, APIs, and backend processing.

### **Key Components**
- **Auto Scaling Group (ASG) of EC2 instances**  
  - Lives in **private subnets** with no direct internet access.  
  - Outbound internet (for updates, package installs, etc.) is typically via a NAT Gateway.

- **ChaosPrivateSubnets**  
  - Private subnets with no route to the internet except through NAT.  
  - Host application servers, background workers, or container hosts (if not using ECS/EKS).

### **Why this matters**
- Protects your compute layer from direct exposure.  
- Auto Scaling ensures resilience and elasticity.  
- Private networking reduces attack surface.

---

## 🗄️ **3. Data Tier (Database Tier)**  
**Purpose:** Provide secure, isolated data storage with controlled access.

### **Key Components**
- **Aurora MySQL Cluster**  
  - Deployed in **isolated subnets** (no internet route, no NAT).  
  - Only reachable from the application tier via security groups.

- **ChaosIsolatedSubnets**  
  - Subnets with **no route to the internet or NAT**.  
  - Used exclusively for databases or sensitive data services.

### **Why this matters**
- Ensures the database is completely isolated from external networks.  
- Reduces risk of data exfiltration or unauthorized access.

---

## 🔐 **Security Model Across Tiers**

### **Network Segmentation**
- **Public → Private → Isolated**  
  - Traffic flows inward only through controlled paths.  
  - No lateral movement between tiers unless explicitly allowed.

### **Security Groups**
- ALB SG allows inbound 443 from the world, outbound to App SG.  
- App SG allows inbound only from ALB SG, outbound to DB SG.  
- DB SG allows inbound only from App SG.

### **No direct internet access**  
- App tier uses NAT Gateway.  
- DB tier has no internet route at all.

---

## 🧩 How the Tiers Work Together

1. **User hits ALB** in public subnets.  
2. **ALB forwards request** to EC2 instances in private subnets.  
3. **App servers query Aurora** in isolated subnets.  
4. **Responses flow back** through the same controlled path.

This is a classic **three‑tier architecture** with strong isolation and high availability.