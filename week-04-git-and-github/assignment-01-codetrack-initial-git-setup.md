# Assignment 1 — CodeTrack: Initial Git Setup (Local Only)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will set up Git correctly on your local machine before starting the CodeTrack project. You will create a local repository and configure your Git identity at both the repository level (local) and the machine level (global). This assignment is local only — you will not push anything to GitHub yet.

---

# Task 1 — Create the CodeTrack Project and Initialize Git

## Goal

Create a `CodeTrack` project folder and initialize it as a Git repository.

### Evidence

#### Screenshot 1 — Output of `git init` inside `CodeTrack` showing "Initialized empty Git repository"

<img width="767" height="382" alt="image" src="https://github.com/user-attachments/assets/bdecd831-4f34-4df5-a528-a4333ec25cd2" />


#### Screenshot 2 — Output of `ls -a` showing the `.git` folder

<img width="612" height="125" alt="image" src="https://github.com/user-attachments/assets/4ff9955b-0551-41ad-a97f-6471c45f98b8" />


### Notes

**1. What is the `.git` folder, and why does it matter?**

The .git folder is the hidden directory that Git creates when a repository is initialized. It stores all the repository's metadata, including commit history, branches, tags, configuration, staging information, and references. This folder is essential because it allows Git to track changes, manage versions, switch between branches, and recover previous versions of files. Without the .git folder, the project is just a normal directory and Git can no longer recognize it as a repository.

# Task 2 — Configure Git Identity Locally (Repository-Only)

## Goal

Set your Git username and email for the `CodeTrack` repository only, using `git config --local`.

### Evidence

<img width="727" height="167" alt="image" src="https://github.com/user-attachments/assets/6c14d570-199e-4068-8ad7-b1cd142ca637" />


#### Screenshot 3 — Output of `git config --local --list` showing your `user.name` and `user.email`

<img width="597" height="222" alt="image" src="https://github.com/user-attachments/assets/406ce0b9-63b1-4663-a7d8-cc1d4cfdedb5" />


# Task 3 — Configure Git Identity Globally

## Goal

Set a global Git username and email for this machine using `git config --global`. Note that CodeTrack's local settings still take priority over these.

### Evidence

<img width="661" height="106" alt="image" src="https://github.com/user-attachments/assets/f4e2cd1c-0256-4817-b001-4856af124e99" />



#### Screenshot 4 — Output of `git config --global --list` showing your `user.name` and `user.email`

<img width="602" height="142" alt="image" src="https://github.com/user-attachments/assets/001035cb-b4e5-42c0-b77a-01ca8634aabc" />


# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [x] `CodeTrack` folder created and initialized as a Git repository (Screenshots 1–2)
- [x] Explanation of the `.git` folder written in your own words
- [x] Local `user.name` and `user.email` configured and verified (Screenshot 3)
- [x] Global `user.name` and `user.email` configured and verified (Screenshot 4)
- [x] No sensitive data exposed

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
