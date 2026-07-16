# Assignment 3 — Building Your Command Center

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a local Claude Skills system by creating the `.claude/skills/` folder structure, adding predefined skill files, and executing a real agentic command (`/scaffold-terraform`) to generate infrastructure code. You will also observe how skills enforce tool restrictions and enable controlled automation.

---

# Task 1 — Create the Skill Folder Structure

## Goal

Create the required `.claude/skills/` directory structure for all skills.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/skills/` folder with all 4 subfolders visible

<img width="377" height="442" alt="Assignment03-image-01" src="https://github.com/user-attachments/assets/4696d29b-d531-49ad-b238-f619cacf2b8e" />

# Task 2 — Add the Skill Files

## Goal

Place all required skill files into their correct directories and verify their configuration.

### Evidence

#### Screenshot 2 — `.claude/skills/scaffold-terraform/` open in VS Code showing both `SKILL.md` and `template-spec.md`

<img width="390" height="303" alt="Assignment03-image-02" src="https://github.com/user-attachments/assets/9891cbae-795b-4c92-93f0-7e8f8aba3ee3" />


#### Screenshot 3 — Screenshot 3 — `tf-plan/SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no Write) and `disable-model-invocation: true`

<img width="1481" height="492" alt="Assignment03-image-12" src="https://github.com/user-attachments/assets/647a2c4f-7b07-4be9-847a-73ed50af390c" />


# Task 3 — Run /scaffold-terraform

## Goal

Execute the `/scaffold-terraform` skill to generate a full Terraform infrastructure setup.

### Evidence

#### Screenshot 4 — Claude's response showing the scaffold complete with the file list

<img width="1136" height="622" alt="Assignment03-image-06" src="https://github.com/user-attachments/assets/b32a52fa-780f-48c0-a149-c86011164318" />


#### Screenshot 5 — VS Code sidebar showing the `terraform/` folder with all generated files inside

<img width="1542" height="701" alt="Assignment03-image-10" src="https://github.com/user-attachments/assets/f2a9f6d2-15a5-4d31-9635-3d4a29061371" />


# Task 4 — Run terraform init and /tf-plan

## Goal

Initialize Terraform and execute the `/tf-plan` skill to observe plan execution and output analysis.

### Evidence

#### Screenshot 6 — Claude's `/tf-plan` response showing it ran the command and analyzed the result (pass or auth error both count)

<img width="1527" height="840" alt="Assignment03-image-11" src="https://github.com/user-attachments/assets/cf18cc41-a860-4f2e-8ab8-7e3fcae4c8cf" />


# Submission Instructions

- Ensure `.claude/skills/` folder and all skill files are committed to your GitHub repository
- Run all commands successfully and capture required screenshots
- Push final changes to your forked repository

---

## GitHub Repository URL

<<<<<<< HEAD
https://github.com/muahmed471/Ultimate-Agentic-DevOps-with-Claude-Code
=======
Paste your forked repository URL here:

`Add your URL here`
>>>>>>> ee02420 (Replace blank-underscore placeholders with explicit "Add your URL here")

## LinkedIn post URL

Paste your forked repository URL here:

<<<<<<< HEAD
https://www.linkedin.com/feed/update/urn:li:ugcPost:7481275829038092288/
=======
`Add your URL here`
---
>>>>>>> ee02420 (Replace blank-underscore placeholders with explicit "Add your URL here")

# Completion Checklist

- [ ] `.claude/skills/` folder created with all 4 skill folders
- [ ] All skill files placed correctly
- [ ] `tf-plan/SKILL.md` shows correct `allowed-tools` restrictions
- [ ] `/scaffold-terraform` executed successfully
- [ ] Terraform files generated inside `terraform/` folder
- [ ] `terraform init` executed successfully
- [ ] `/tf-plan` executed and output analyzed by Claude
- [ ] All required screenshots added
- [ ] GitHub repository URL included
- [ ] LinkedIn post URL included

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
