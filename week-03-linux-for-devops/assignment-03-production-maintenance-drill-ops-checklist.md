# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

<img width="1202" height="622" alt="image" src="https://github.com/user-attachments/assets/68afcafa-54a2-435b-a93a-dacb5b401349" />


#### Screenshot 2 — Output of `ip a`

<img width="1121" height="332" alt="image" src="https://github.com/user-attachments/assets/4eb30d78-54de-4dfa-b154-e2dfcd4115a8" />


#### Screenshot 3 — Output of `sudo ss -tulpen`

<img width="1842" height="532" alt="image" src="https://github.com/user-attachments/assets/8026ac48-8df0-44a1-9cf4-aed125bc6484" />


#### Screenshot 4 — Output of `sudo ufw status`

<img width="467" height="80" alt="image" src="https://github.com/user-attachments/assets/c3254a5e-6f59-4e0b-a4fb-46803acf73d4" />


### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

Process name: Nginx Listening port: 80 proves Nginx listening on port 0.0.0.0:80

**2. What proves SSH is active on port 22?**

Connectivity to the server via SSH (inbound rule) proves the port is active on 22 able to do the SSH.

**3. Did you find any unexpected open ports? Explain briefly.**

I can see DNS port 53 open and also port number 68 and 323 for DNS, Systemd and Chronyd respectiviely.

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

<img width="1445" height="426" alt="image" src="https://github.com/user-attachments/assets/557c09ff-e0cf-4f2a-92d7-030c8dcc4568" />


#### Screenshot 2 — Output of `sudo nginx -t`

<img width="797" height="96" alt="image" src="https://github.com/user-attachments/assets/cbcf155a-95cb-45e1-acfb-15bb1dda1c2d" />


#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

<img width="1852" height="122" alt="image" src="https://github.com/user-attachments/assets/a369c3b2-d804-4f6b-a7c9-2b550c1a568b" />


### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart in production, the impact depends on how it is being used whether as a web server, reverse proxy, or load balancer. Nginx is the only entry point to your application:
1. Users cannot access the website or API.
2. Requests fail with connection errors or timeouts.
3. Monitoring tools report the service as unavailable.

**2. What's your basic rollback plan?**

First check the status and follow the below steps by checking
Nginx configuration error
SSL certificate issue
Backend application issue
Port conflict

If you have a backup then restore it.

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

<img width="1907" height="581" alt="image" src="https://github.com/user-attachments/assets/aaf3190a-6f42-49cc-bf47-d3ec15c8b183" />


#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

<img width="857" height="72" alt="image" src="https://github.com/user-attachments/assets/c2da1958-8013-4a72-9276-dd70b536ac11" />


#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

<img width="1437" height="202" alt="image" src="https://github.com/user-attachments/assets/af18f7bb-cb5d-4975-93fa-cd560888c408" />


### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

Yes I can see one error in the log and it's about.

When Nginx is reloaded, the new master process inherits the listening sockets port 80 from the old master process instead of closing and reopening them.

**2. If there were no errors, what does that indicate about the system?**

If there are no errors, it indicates that the Nginx service started or reloaded successfully, the configuration is valid, and Nginx is listening for incoming requests. However, I would still verify end-to-end functionality by checking the service status, testing the application URL, and confirming that backend services are responding correctly

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes I can see them in plog entries. Below is the traffice flow status.

tail -f /var/log/nginx/access.log

127.0.0.1 - - [17/Jul/2026:05:35:10 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/8.5.0"

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

<img width="735" height="102" alt="image" src="https://github.com/user-attachments/assets/8ce4e841-6cfb-4a22-abe8-dd7e75184346" />


#### Screenshot 2 — Output of `free -h`

<img width="951" height="122" alt="image" src="https://github.com/user-attachments/assets/0efb263d-0d92-4206-bbee-7f5eadd01ed5" />


#### Screenshot 3 — Output of `df -h`

<img width="937" height="350" alt="image" src="https://github.com/user-attachments/assets/44f8310e-1332-448e-8a34-f61a62331def" />


#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

<img width="630" height="446" alt="image" src="https://github.com/user-attachments/assets/d7892641-4350-4f7c-ac7a-8827c4ddbbb7" />

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

I couldn't see any critical resource, but I can say RAM is a bit more consumed other than CPU and Disk.

**2. What happens if disk becomes 100% full in a production server?**

it can have severe consequences depending on what is stored on that filesystem. 
Common impacts include
Applications Stop Working
Applications cannot write logs, temporary files, or uploaded data.
Users may receive 500 Internal Server Error or similar failures.

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

<img width="777" height="290" alt="image" src="https://github.com/user-attachments/assets/a2cd8ee8-1120-486f-ac32-3370c9d33baf" />


#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

<img width="1895" height="772" alt="image" src="https://github.com/user-attachments/assets/e1bd87e2-5097-4d03-af92-fb02f8031b07" />


#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

<img width="962" height="282" alt="image" src="https://github.com/user-attachments/assets/4ee5a9df-bea0-4a45-8a73-06d0c6451e91" />


### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

Write your answer here.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

Add your screenshot here.

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

Add your screenshot here.

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

Write your answer here.

---

**2. How did you fix the issue?**

Write your answer here.

---

**3. How can you avoid this kind of issue in real production systems?**

Write your answer here.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

Add your screenshot here.

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

Write your answer here

---

**2. How did you fix the issue and restore the application?**

Write your answer here.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

Write your answer here.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

Write your answer here.

---

**2. Why should only required ports be open on a production server?**

Write your answer here.

---

**3. Why is it important for Nginx to be enabled on boot?**

Write your answer here.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Write your answer here.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Write your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`__________________________`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
