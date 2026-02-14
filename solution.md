# AWS Auto Scaling – Solution Guide

## Step 1: Create Launch Template

- Name: my-ag-template
- AMI: Ubuntu (Free Tier Eligible)
- Instance Type: t2.micro or t3.micro
- Select Key Pair

### User Data Script

#!/bin/bash
apt update -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
cd /var/www/html
echo "This is server" > index.html

Create Launch Template.

---

## Step 2: Create Auto Scaling Group

- Name: my-new-ag
- Select Launch Template created above
- Select multiple Availability Zones
- No Load Balancer (for this lab)

---

## Step 3: Configure Capacity

- Desired Capacity: 2
- Minimum Capacity: 1
- Maximum Capacity: 3

---

## Step 4: Configure Scaling Policy

- Policy Type: Target Tracking
- Metric Type: Average CPU Utilization
- Target Value: 60%

Create Auto Scaling Group.

---

## Step 5: Verify Instances

Go to EC2 Dashboard.
You should see 2 instances running.

If you manually terminate one instance,
Auto Scaling Group will automatically launch a new instance.

---

## Step 6: Generate Load

SSH into EC2 instance and run:

top

Then generate CPU load:

yes > /dev/null &

Run on multiple servers to increase load.

When CPU exceeds 60%,
Auto Scaling will launch a new instance automatically.

---

## Step 7: Observe Scaling

- CPU increases → New instance launched
- CPU decreases → Instance terminated (after cooldown period)

---

## ✅ Outcome

Successfully implemented:

- Launch Template
- Auto Scaling Group
- Dynamic scaling based on CPU
- Self-healing infrastructure

NavOps Academy
