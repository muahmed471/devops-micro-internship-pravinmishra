# Assignment 5 — Open-Source Collaboration: Fork, Clone, Sync & Pull Request

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will contribute one small documentation change to a shared repository using a standard open-source collaboration workflow: fork, clone, configure remotes, branch, commit, sync with upstream, push, and open a Pull Request. This is a different, separate practice repository from the one you submit your DMI work in.

---

# Task 0 — Fork the Upstream Repository

## Goal

Fork `pravinmishraaws/devops-micro-internship-interviews` into your own GitHub account.

### Evidence

#### Screenshot 1 — Your fork page with your username and `devops-micro-internship-interviews` visible in the browser URL

<img width="1891" height="1097" alt="Assigment05-Screenshot2" src="https://github.com/user-attachments/assets/4a7c9c89-4eac-4b99-876b-b1ab3f36f2b4" />


# Task 1 — Authenticate GitHub from the Terminal

## Goal

Configure one authentication method — HTTPS with a Personal Access Token, or SSH — so you can push to your fork. Use only one method.

### Evidence

#### Screenshot 2 — Output of `git config --global --get credential.helper` (HTTPS) or `ssh -T git@github.com` (SSH) showing successful authentication — never show your token or private key

<img width="1795" height="837" alt="Assigment05-Screenshot3" src="https://github.com/user-attachments/assets/2524d49e-6f41-4b4f-a16b-c509c40975d4" />


# Task 2 — Clone Your Fork and Configure Remotes

## Goal

Clone your fork locally, then add the original repository as `upstream`.

### Evidence

#### Screenshot 3 — Output of `git remote -v` showing `origin` pointing to your fork and `upstream` pointing to `pravinmishraaws/devops-micro-internship-interviews`

<img width="1075" height="130" alt="Assigment05-Screenshot5" src="https://github.com/user-attachments/assets/ace37c52-0cdf-4836-87cf-f469b5ee02d9" />


# Task 3 — Create a Feature Branch and Make Your Change

## Goal

Create the branch `feature-readme-update`, add only your own entry (`Full Name — Group <Group Name/Number>`) to the Student List at the end of `pull_request.md`, and commit it with the message `docs: add my name to student list`.

### Evidence

#### Screenshot 4 — Output of `git status` showing `pull_request.md` modified before staging

<img width="1100" height="207" alt="Assigment05-Screenshot6" src="https://github.com/user-attachments/assets/aa404e4d-bdc9-47a4-a275-3b6638201500" />


#### Screenshot 5 — Output of `git commit`

<img width="1125" height="186" alt="Assigment05-Screenshot7" src="https://github.com/user-attachments/assets/3ac3348a-d33c-48f9-9f2c-ab4e01b9d394" />


# Task 4 — Synchronize with Upstream and Push to Your Fork

## Goal

Fetch and merge `upstream/main` into your local default branch, rebase your feature branch onto it, then push `feature-readme-update` to your fork.

### Evidence

#### Screenshot 6 — Output of `git push -u origin feature-readme-update` showing a successful push

<img width="1026" height="327" alt="Assigment05-Screenshot8" src="https://github.com/user-attachments/assets/6f1c9d25-f404-400b-91fd-2f6dd2b866f3" />


#### Screenshot 7 — Your fork on GitHub showing `feature-readme-update` in the branch selector or a "Compare & pull request" banner

<img width="1885" height="1086" alt="Assigment05-Screenshot10" src="https://github.com/user-attachments/assets/08a7ac6d-9ecc-4e42-a6aa-6fed3be7a97f" />


# Task 5 — Create a Pull Request to Upstream

## Goal

Open a Pull Request from `feature-readme-update` on your fork to `main` on the upstream repository, using the title `docs: add my name to student list`.

### Evidence

<<<<<<< HEAD
#### Screenshot 8 — Pull Request creation page showing the correct base repository/branch and head repository/branch
=======
#### Screenshot 8 — Pull Request creation page showing the correct base repository, base branch, head repository, compare branch, and title
>>>>>>> upstream/main

<img width="1760" height="1085" alt="Assigment05-Screenshot9" src="https://github.com/user-attachments/assets/c4654aeb-4dbf-470d-b74c-7c93aba7acc5" />


#### Screenshot 9 — Successfully created Pull Request page with the PR number visible

<img width="1772" height="1030" alt="Assigment05-Screenshot11" src="https://github.com/user-attachments/assets/40b6645d-3f48-4659-98ae-791c9942ca60" />


#### Pull Request URL

Paste your Pull Request URL here:

https://github.com/pravinmishraaws/devops-micro-internship-interviews/pull/435

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/muneer-ahmed-25322b206_devops-git-github-activity-7488111782096650241-30IC?utm_source=share&utm_medium=member_desktop&rcm=ACoAADRb5Z8BfmU5GnTuVjG5eHP-d8cMT-AYl0c

#### Screenshot — LinkedIn post showing your successfully created Pull Request

<img width="672" height="927" alt="Assigment05-Screenshot12" src="https://github.com/user-attachments/assets/273c70f1-66ea-4e10-9516-241f3759c196" />


# Submission Instructions

- Add all required screenshots in your submission
- Do not expose a Personal Access Token, SSH private key, password, or authentication secret
- Only your own entry in `pull_request.md` may be added — do not edit or delete another student's entry
- Include your fork URL and Pull Request URL

---

## Fork URL

Paste your fork URL here:

https://github.com/muahmed471/devops-micro-internship-interviews

# Completion Checklist

- [x] Upstream repository forked to your GitHub account (Screenshot 1)
- [x] GitHub authentication configured securely (Screenshot 2)
- [x] Fork cloned locally with `origin` and `upstream` configured (Screenshot 3)
- [x] Only `pull_request.md` modified, with your own entry added (Screenshots 4–5)
- [x] Local default branch synchronized with `upstream/main`, feature branch rebased and pushed (Screenshots 6–7)
- [x] Pull Request opened against the correct upstream repository and branch (Screenshots 8–9)
- [x] Fork URL and Pull Request URL included
- [x] LinkedIn post published and URL submitted
- [x] No PAT, password, private key, or authentication secret exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

<<<<<<< HEAD
- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
=======
- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
>>>>>>> upstream/main
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
