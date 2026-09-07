# Assignment 5 — Deploy a Highly Available Two-Tier Application on AWS

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will design and deploy a highly available two-tier web application on AWS: highly available networking across two Availability Zones, an Application Load Balancer, an Auto Scaling Group for the web tier, and a private Multi-AZ RDS database. You must prove high availability with real failure tests.

---

# Task 1 — Create HA Networking (VPC + 4 Subnets + IGW + NAT + Route Tables)

## Goal

Build a VPC (10.0.0.0/16) with two public and two private subnets across two Availability Zones, an Internet Gateway, a NAT Gateway, and the matching public/private route tables.

### Evidence

#### Screenshot 1 — VPC details showing CIDR 10.0.0.0/16

![screenshot](./screenshots/Assignment5-Screenshot1.png)
![screenshot](./screenshots/Assignment5-Screenshot2.png)

#### Screenshot 2 — Subnets list showing four subnets and their Availability Zones

![screenshot](./screenshots/Assignment5-Screenshot3.png)

#### Screenshot 3 — Public route table showing the Internet Gateway route and both public-subnet associations

![screenshot](./screenshots/Assignment5-Screenshot5.png)
![screenshot](./screenshots/Assignment5-Screenshot4.png)
![screenshot](./screenshots/Assignment5-Screenshot6.png)

#### Screenshot 4 — Private route table showing the NAT Gateway route and both private-subnet associations

![screenshot](./screenshots/Assignment5-Screenshot7.png)

#### Screenshot 5 — NAT Gateway status showing Available and the Elastic IP

![screenshot](./screenshots/Assignment5-Screenshot8.png)
![screenshot](./screenshots/Assignment5-Screenshot9.png)

# Task 2 — Create Security Groups (ALB, EC2, RDS) with Least Privilege

## Goal

Create `ha-alb-sg` (HTTP public), `ha-web-sg` (HTTP only from `ha-alb-sg`, SSH from your IP), and `ha-db-sg` (database port only from `ha-web-sg`).

### Evidence

#### Screenshot 6 — ALB Security Group inbound rules

![screenshot](./screenshots/Assignment5-Screenshot10.png)

#### Screenshot 7 — EC2 Security Group inbound rules showing the ALB Security Group reference and SSH from your IP

![screenshot](./screenshots/Assignment5-Screenshot11.png)

#### Screenshot 8 — RDS Security Group inbound rule showing the database port allowed only from the EC2 Security Group

![screenshot](./screenshots/Assignment5-Screenshot12.png)

# Task 3 — Deploy Database Tier (RDS Multi-AZ in Private Subnets)

## Goal

Launch a private, Multi-AZ RDS database (MySQL or PostgreSQL) using the private DB Subnet Group and `ha-db-sg`.

### Evidence

#### Screenshot 9 — RDS summary showing Multi-AZ = Yes and Publicly accessible = No

![screenshot](./screenshots/Assignment5-Screenshot14.png)

#### Screenshot 10 — RDS connectivity section showing the DB Subnet Group and Security Group

![screenshot](./screenshots/Assignment5-Screenshot15.png)

# Task 4 — Build a Launch Template (User Data Installs App + Connects to DB)

## Goal

Create a Launch Template whose user data installs the web-server runtime, deploys the application, configures the database connection, and starts the required services.

### Evidence

#### Screenshot 11 — Launch Template details showing that user data exists, including a visible snippet

![screenshot](./screenshots/Assignment5-Screenshot16.png)

#### Screenshot 12 — A running instance created from the template showing the application responds on port 80

![screenshot](./screenshots/Assignment5-Screenshot17.png)

# Task 5 — Create an Application Load Balancer (ALB) Across 2 Public Subnets

## Goal

Create an internet-facing ALB across both public subnets with an HTTP listener and a healthy instance target group.

### Evidence

#### Screenshot 13 — ALB details showing two public subnets in two Availability Zones

![screenshot](./screenshots/Assignment5-Screenshot18.png)
![screenshot](./screenshots/Assignment5-Screenshot19.png)

#### Screenshot 14 — Target group showing at least one healthy target

![screenshot](./screenshots/Assignment5-Screenshot20.png)

# Task 6 — Create Auto Scaling Group (ASG) in 2 Public Subnets

## Goal

Create an Auto Scaling Group from the Launch Template across both public subnets, with desired capacity 2, minimum 2, and maximum 4, registered to the ALB target group.

### Evidence

#### Screenshot 15 — Auto Scaling Group showing desired, minimum, and maximum capacity and the selected subnet Availability Zones

![screenshot](./screenshots/Assignment5-Screenshot21.png)

#### Screenshot 16 — EC2 instances list showing two running instances in different Availability Zones

![screenshot](./screenshots/Assignment5-Screenshot22.png)

# Task 7 — Configure App to Use RDS + Validate Read/Write

## Goal

Confirm the application communicates with the RDS database through the ALB DNS name with at least one read and one write operation.

### Evidence

#### Screenshot 17 — Browser showing the application loaded through the ALB DNS name with the URL visible

![screenshot](./screenshots/Assignment5-Screenshot23.png)
![screenshot](./screenshots/Assignment5-Screenshot24.png)

#### Screenshot 18 — Proof of a database write through a UI message or database query output

![screenshot](./screenshots/Assignment5-Screenshot25.png)

# Task 8 — High Availability Tests (Must Do Both)

## Goal

Test A: terminate one web instance and confirm the Auto Scaling Group replaces it automatically without interrupting the ALB. Test B: simulate an Availability Zone impact (stop, detach, or reduce desired capacity in one AZ) and confirm the application stays available.

### Evidence

#### Screenshot 19 — EC2 showing the terminated instance and the newly launched instance

![screenshot](./screenshots/Assignment5-Screenshot26.png)

#### Screenshot 20 — Target group showing healthy targets after replacement

![screenshot](./screenshots/Assignment5-Screenshot27.png)

#### Screenshot 21 — Evidence that an instance was removed, detached, placed in Standby, or stopped in one Availability Zone

![screenshot](./screenshots/Assignment5-Screenshot28.png)

#### Screenshot 22 — Browser showing that the ALB DNS endpoint still works during the change

![screenshot](./screenshots/Assignment5-Screenshot29.png)

# Task 9 — Architecture and Test-Results Summary

## Goal

Summarize the VPC/subnet layout, the ALB and Auto Scaling Group setup, the private Multi-AZ RDS setup, and the results of both high-availability tests.

### Evidence

#### Screenshot 23 — A simple architecture diagram (hand-drawn is fine), or an AWS console overview showing the components

![screenshot](./screenshots/Assignment5-Screenshot30.png)

### Notes

Write a short summary covering the network, ALB/ASG setup, RDS setup, and the results of Test A and Test B.

The high-availability web application was deployed in a custom AWS VPC across two Availability Zones (ap-south-2a and ap-south-2b), using public subnets for the web servers and private subnets for backend resources. NAT Gateways provide outbound internet access from the private subnets.

An internet-facing Application Load Balancer (ha-alb-EpicReads) was configured with an HTTP listener on port 80 and connected to the ha-web-tg target group. An Auto Scaling Group using the ha-web-launch-template was configured with Desired = 2, Minimum = 2, Maximum = 4, distributing EC2 instances across both Availability Zones. ELB health checks were enabled, and the targets became healthy.

Amazon RDS for MySQL was configured in the private subnet with the appdb database. The PHP application successfully connected to RDS and displayed the database connection as SUCCESS.

Test A – Application Availability: The ALB DNS endpoint was tested and initially experienced a timeout while the backend web server was being corrected. After fixing the Apache/PHP/database issue, the application successfully loaded through the ALB.

Test B – High Availability: The application was verified through the target group with healthy EC2 targets across the Availability Zones, demonstrating that the ALB and Auto Scaling configuration can distribute traffic and maintain application availability.

Overall result: The application is successfully deployed as a highly available, scalable, and secure AWS web application using VPC, ALB, ASG, EC2, NAT Gateway, and RDS MySQL.

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post about the high-availability build, including the ALB URL (or a redacted screenshot), three to five lines on what you built and how you tested high availability, and one proof screenshot.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://lnkd.in/p/dYhpb7SY

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Do not expose passwords, connection strings, private keys, or account IDs

---

# Completion Checklist

- [ ] Task 1: VPC, four subnets, IGW, NAT Gateway, and route tables created (Screenshots 1–5)
- [ ] Task 2: Least-privilege ALB, EC2, and RDS security groups created (Screenshots 6–8)
- [ ] Task 3: Private Multi-AZ RDS created (Screenshots 9–10)
- [ ] Task 4: Self-configuring Launch Template created and tested (Screenshots 11–12)
- [ ] Task 5: ALB created across both public subnets (Screenshots 13–14)
- [ ] Task 6: Auto Scaling Group running two instances across two AZs (Screenshots 15–16)
- [ ] Task 7: Application verified through the ALB with a database read and write (Screenshots 17–18)
- [ ] Task 8: Both high-availability tests completed (Screenshots 19–22)
- [ ] Task 9: Architecture and test-results summary completed (Screenshot 23 & Notes)
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
