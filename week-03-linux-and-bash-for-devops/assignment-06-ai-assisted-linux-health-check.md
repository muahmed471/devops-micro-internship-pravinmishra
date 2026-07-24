# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

<img width="582" height="282" alt="image" src="https://github.com/user-attachments/assets/f011a3a9-ae5c-4d26-b9ca-6c3bc4bdaa5b" />


#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

<img width="1105" height="836" alt="image" src="https://github.com/user-attachments/assets/d1a0f33c-a5f9-403b-8244-5f0caa7a8196" />


### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

By running systemctl status nginx command provides the status as active (running) proves that Nginx is running. 

**2. What proves that the server is listening for HTTP traffic?**

Running the command ss -tuln | grep :80 (or netstat -tuln | grep :80) shows that port 80 is in the LISTEN state. This confirms that the server is listening for incoming HTTP traffic.


**3. Why must you capture a healthy baseline before simulating an incident?**

Capturing a healthy baseline helps verify that the system is functioning correctly before any changes are made. It provides a reference point to compare against after simulating an incident, making it easier to identify issues, troubleshoot problems, and confirm that the system has been successfully restored.

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

<img width="1702" height="837" alt="image" src="https://github.com/user-attachments/assets/8abaf325-19b5-47dc-8e7c-be1762aa53a0" />


### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Project-specific operational rules help Claude understand the application's architecture, team standards, and approved procedures. This ensures it provides accurate, consistent, and safe guidance that aligns with the project's requirements while avoiding actions that could violate organizational policies.

**2. Why is the human required to execute the recovery command?**

A human must execute the recovery command because recovery actions can directly affect production systems and business operations. Human approval provides oversight, verifies that the proposed action is appropriate, and prevents accidental or unsafe changes made without proper authorization.

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The rule that requires evidence before conclusions prevents Claude from making an unsupported diagnosis. Claude should rely on logs, metrics, monitoring data, and other verified evidence, and if there isn't enough information, it should state the uncertainty and request additional data instead of guessing.

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

<img width="1851" height="840" alt="image" src="https://github.com/user-attachments/assets/8d297cfc-52c2-4b16-b035-fa6519c93438" />


### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The Gather phase is when Claude inspects the repository, reviews the project structure, configuration files, dependencies, tests, and Git status without making any changes. It collects information to understand the project before suggesting any actions.

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Yes. Claude only performed a read-only inspection and did not create or modify any files. I verified this by checking the Git status (git status), which showed no changes, and by confirming that no new files appeared in the repository.

**3. Why is planning before coding useful in DevOps automation?**

Planning before coding helps identify the project requirements, dependencies, and potential risks before making changes. This reduces errors, avoids unnecessary modifications, and ensures automation is implemented in a safe, efficient, and reliable manner.

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

<img width="780" height="717" alt="image" src="https://github.com/user-attachments/assets/e21224e6-504e-4823-a989-eeb4fd2491a7" />


#### Screenshot 6 — Middle section showing check functions and conditionals

<img width="957" height="845" alt="image" src="https://github.com/user-attachments/assets/6723c490-a11d-4c15-92a1-ee7127940572" />


#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

<img width="1010" height="846" alt="image" src="https://github.com/user-attachments/assets/41b2f444-a417-4620-8a83-48b7bf2fc8a6" />


#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

<img width="707" height="102" alt="image" src="https://github.com/user-attachments/assets/65eb2aa2-97c3-4812-b700-86e0dea4d957" />


### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the health check functions that the script needs to run. Each item represents a specific system check, such as CPU, memory, disk, or service status.

**2. How does the `for` loop use that array?**

The for loop goes through each item in the checks array one by one and executes the corresponding health check function. This allows the script to perform all checks automatically without repeating code.

**3. Why are the health checks separated into functions?**

Separating the health checks into functions makes the script more organized, easier to read, and simpler to maintain. It also allows individual checks to be updated, tested, or reused without affecting the rest of the script.

**4. What is the purpose of `$(...)` in this script?**

$(...) is used for command substitution. It runs a command and captures its output so the result can be assigned to a variable or used as part of another command.

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes allow other programs or automation tools to understand the script's result. A success code indicates the system is healthy, while warning and failure codes signal increasing levels of concern, enabling monitoring tools or CI/CD pipelines to take appropriate actions automatically.

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

<img width="767" height="457" alt="image" src="https://github.com/user-attachments/assets/e6b802df-8a77-4db6-a86a-713fb0d6cb8a" />


#### Screenshot 10 — Output showing the captured exit code and final summary

<img width="997" height="457" alt="image" src="https://github.com/user-attachments/assets/655fab3c-6a13-4065-b424-f211795c2127" />


### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The overall status of my healthy baseline is HEALTHY. All required system and application health checks completed successfully, indicating that the server and application are operating normally.

**2. Which exact Linux evidence proves the application is serving traffic?**

The application is proven to be serving traffic by a successful HTTP response from the application endpoint. Running a command such as curl http://localhost:<port> returned the expected response (for example, HTTP 200 OK), confirming that the application is accessible and responding to requests.

**3. Did your script return exit code 0 or 1? Explain why.**

My script returned exit code 0 because all health checks passed successfully and no critical failures were detected. An exit code of 0 indicates that the system is healthy and operating as expected.

**4. What is the difference between a warning and a failure in this script?**

A warning indicates a non-critical issue, such as a resource approaching its threshold, while the system continues to function normally. A failure indicates a critical problem, such as an unavailable service or failed health check, that may impact the application's operation and requires immediate attention.

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

Add your screenshot here.

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

Add your answer here.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

Add your answer here.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Add your answer here.

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

Add your answer here.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

Add your screenshot here.

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

Add your screenshot here.

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

Add your answer here.

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

Add your answer here.

---

**3. Did Claude execute the recovery command? Why is that important?**

Add your answer here.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

Add your answer here.

---

**5. Which phase is represented by Claude's explanation?**

Add your answer here.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

Add your screenshot here.

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

Add your screenshot here.

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

Add your screenshot here.

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

Add your answer here.

---

**2. What evidence proves that the service recovered?**

Add your answer here.

---

**3. Why is the second triage run necessary?**

Add your answer here.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

Add your answer here.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

Add your answer here.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Add your full name here

**Date:** DD/MM/YYYY

---

**1. Reported Symptom**

Add your answer here.

---

**2. Evidence Collected**

Add your answer here.

---

**3. Most Likely Cause**

Add your answer here.

---

**4. Human-Approved Recovery Action**

Add your answer here.

---

**5. Verification**

Add your answer here.

---

**6. Safety Decision**

Add your answer here.

---

**7. Agentic Loop Mapping**

Add your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`Add your URL here`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
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
