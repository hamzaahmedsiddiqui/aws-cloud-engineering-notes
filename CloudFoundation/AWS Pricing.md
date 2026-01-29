# AWS Pricing basics
![Alt text](/images/pricing.png)
This document explains **AWS pricing from the ground up**, written for students.
Clear concepts, exam-ready language, no fluff.

---

## What Is AWS Pricing?

Amazon Web Services (AWS) follows a **pay-as-you-go pricing model**.

This means:
- No upfront infrastructure cost
- No long-term contracts (unless you choose them)
- You pay only for the resources you actually consume

AWS pricing works like a utility bill:
- Use more → pay more
- Use less → pay less
- Stop using → stop paying

---

## Fundamental Drivers of AWS Cost

AWS pricing is based on **three fundamental cost drivers**:

### 1. Compute
- Charged by the **second or hour**
- Cost depends on:
  - Instance type
  - Instance size
  - Operating system
- Examples:
  - EC2
  - Lambda
  - ECS

**In simple terms:**  
How long did CPU and memory run?

---

### 2. Storage
- Charged **per GB**
- Cost varies by:
  - Storage type
  - Durability
  - Access frequency
- Examples:
  - S3
  - EBS
  - EFS

**In simple terms:**  
How much data is stored, and for how long?

---

### 3. Data Transfer
- Inbound data transfer: **usually free**
- Outbound data transfer: **charged**
- Charged per GB
- Outbound data is aggregated across services
- Appears on the bill as **Data Transfer Out**

**In simple terms:**  
How much data leaves AWS?

---

## How Do You Pay for AWS?

AWS uses a **utility-based pricing philosophy**.

### Core Pricing Principles

### 1. Pay for what you use
- No upfront payments
- Start or stop services anytime
- No long-term contracts required

### 2. Pay less when you reserve
- Commit to predictable usage
- Receive discounted pricing

### 3. Pay less as you use more
- Volume-based discounts
- AWS regularly reduces prices as it scales

---

## Pay for What You Use: On-Premises vs AWS

### Traditional On-Premises Model
- Pay upfront for hardware
- Infrastructure sized for peak demand
- Idle resources still cost money
- High capital expense (CapEx)

### AWS Cloud Model
- Pay only for consumed resources
- Scale up or down instantly
- No idle infrastructure cost
- Operational expense (OpEx)

**Result:**  
Lower risk, better flexibility, and reduced waste.

---

## AWS Pricing Models

AWS offers multiple pricing models to match different workloads.

### 1. On-Demand Pricing
- Pay per second or hour
- No commitment
- Best for:
  - Short-term workloads
  - Unpredictable traffic
  - Testing and development

---

### 2. Reserved Instances (RI)
Used mainly for EC2 and RDS.

Reserved Instances are available in three payment options:

#### a. All Upfront Reserved Instance (AURI)
- Pay everything upfront
- **Highest discount**

#### b. Partial Upfront Reserved Instance (PURI)
- Pay part upfront
- **Medium discount**

#### c. No Upfront Reserved Instance (NURI)
- No upfront payment
- **Lowest discount**

**Rule to remember:**  
More commitment = more savings

---

### 3. Savings Plans
- Commit to a consistent usage amount ($/hour)
- Flexible across instance families and regions
- Applies to:
  - EC2
  - Lambda
  - Fargate

---

### 4. Spot Instances
- Use spare AWS capacity
- Up to **90% cheaper** than On-Demand
- Can be interrupted
- Best for:
  - Batch jobs
  - Big data processing
  - Fault-tolerant workloads

---

## AWS Free Tier

AWS Free Tier allows users to **learn and experiment at low or no cost**.

### Types of Free Tier

### 1. Always Free
Available as long as the account exists.
- Example:
  - S3: limited storage
  - Lambda: 1 million requests/month

### 2. 12-Month Free
Valid for the first 12 months after account creation.
- Example:
  - EC2: 750 hours/month of small instances
  - RDS: 750 hours/month

### 3. Trials
Short-term free usage for specific services.

**Important:**  
Free Tier has usage limits.  
Exceed the limit → you are charged.

---

## Total Cost of Ownership (TCO)

**TCO means the total cost of running IT systems over time.**

### Traditional (On-Premises) TCO Includes:
- Hardware purchase
- Data center space
- Power and cooling
- Maintenance
- IT staff
- Hardware refresh

### AWS TCO Includes:
- Service usage
- Data transfer
- Optional support plans

### Why AWS Often Has Lower TCO
- No idle infrastructure
- No hardware lifecycle management
- Reduced operational overhead

**Key shift:**  
Capital expense (CapEx) → Operational expense (OpEx)

---

## AWS Pricing and Cost Tools

AWS provides tools to help estimate and optimize costs.

### 1. AWS Pricing Calculator
- Estimate monthly costs before deployment
- Compare pricing options
- Plan budgets

---

### 2. AWS Cost Explorer
- Analyze past usage
- Identify cost trends
- Detect unused resources

---

### 3. AWS Budgets
- Set spending limits
- Get alerts when thresholds are exceeded

---

## Key Exam Takeaways

- AWS pricing is **pay-as-you-go**
- Three cost drivers:
  - Compute
  - Storage
  - Outbound data transfer
- Inbound data is usually free
- Reserved usage lowers cost
- Free Tier is usage-limited
- AWS shifts cost from CapEx to OpEx

