# Assignment 5 — Open-Source Collaboration: Fork, Sync & Pull Request

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will fork the upstream repository, authenticate GitHub access, clone your fork, configure remotes, create a feature branch, update `pull_request.md`, synchronize with upstream, push your branch, and create a Pull Request.

---

# Task 0 — Fork the Upstream Repository

## Goal

Create a copy of the upstream repository under your GitHub account.

### Evidence

#### Screenshot 1 — Your fork page with your username and `devops-micro-internship-interviews` visible in the browser URL

<img width="1891" height="1097" alt="image" src="https://github.com/user-attachments/assets/ddaafde3-7ba5-492d-b538-23c45e934609" />


# Task 1 — Authenticate GitHub from the Terminal

## Goal

Configure one secure authentication method so you can push changes from your terminal to your GitHub fork. Complete only one method: HTTPS with a Personal Access Token or SSH authentication.

### Evidence — Choose One

#### Screenshot 2 (HTTPS) — Output of `git config --global --get credential.helper`

Add your screenshot here if you used HTTPS. Do not show your Personal Access Token.

<img width="1795" height="837" alt="image" src="https://github.com/user-attachments/assets/580a0e1a-9412-435b-94ec-e090afa4b895" />


**OR**

#### Screenshot 2 (SSH) — Output of `ssh -T git@github.com` showing successful authentication and your own GitHub username

<img width="1065" height="105" alt="image" src="https://github.com/user-attachments/assets/e0c66165-0710-4e6f-a781-b7b418f40596" />


# Task 2 — Clone Your Fork Locally and Configure Remotes

## Goal

Create a local working copy where `origin` points to your fork and `upstream` points to the original repository.

### Evidence

#### Screenshot 3 — Output of `git remote -v` showing `origin` and `upstream` correctly

<img width="1075" height="130" alt="image" src="https://github.com/user-attachments/assets/e481d2ad-095c-40a1-9838-ae36959d9fe4" />


# Task 3 — Create a Feature Branch and Make Your Change

## Goal

Create the required `feature-readme-update` branch and add only your own entry to `pull_request.md`.

### Evidence

#### Screenshot 4 — Output of `git status` showing `pull_request.md` modified before staging

<img width="1100" height="207" alt="image" src="https://github.com/user-attachments/assets/99c2a33b-9198-4a0a-bcd6-8bb7c92d024b" />

#### Screenshot 5 — Output of `git commit -m "docs: add my name to student list"`

<img width="1125" height="186" alt="image" src="https://github.com/user-attachments/assets/f5f5e5c5-effd-4b92-807b-0f0e92646603" />


# Task 4 — Synchronize with Upstream and Push to Your Fork

## Goal

Update your local default branch from upstream, rebase the feature branch, and push it to `origin`.

### Evidence

#### Screenshot 6 — Output of `git push -u origin feature-readme-update` showing a successful push

<img width="1026" height="327" alt="image" src="https://github.com/user-attachments/assets/5a0f0789-54e8-4301-99cd-c009db3c65c1" />


#### Screenshot 7 — Your fork on GitHub showing `feature-readme-update` in the branch selector or a Compare & pull request banner

<img width="1885" height="1086" alt="image" src="https://github.com/user-attachments/assets/122dad50-797a-4279-bc6f-19ea286cedfa" />



# Task 5 — Create a Pull Request to Upstream

## Goal

Open a Pull Request from your fork’s feature branch to the upstream `main` branch.

### Required Pull Request Details

- Base repository: `pravinmishraaws/devops-micro-internship-interviews`
- Base branch: `main`
- Head repository: `muahmed471/devops-micro-internship-interviews`
- Compare branch: `feature-readme-update`
- PR Title: `docs: add my name to student list`
- PR Body: `This PR adds my name to the Student List in pull_request.md as part of the DMI GitHub collaboration assignment.`

### Evidence

#### Screenshot 8 — Pull Request creation page showing the correct base repository, base branch, head repository, compare branch, and title

<img width="1897" height="1087" alt="image" src="https://github.com/user-attachments/assets/df273b57-184d-47de-bd4e-253666a3ac06" />


#### Screenshot 9 — Successfully created Pull Request page with the PR number visible

<img width="1772" height="1030" alt="image" src="https://github.com/user-attachments/assets/d0efc5d0-5834-431d-9f77-7b50fbe37e26" />


# Required URLs

#### Fork URL

https://github.com/muahmed471/devops-micro-internship-interviews

#### Pull Request URL

https://github.com/pravinmishraaws/devops-micro-internship-interviews/pull/435

# LinkedIn Post (Mandatory)

Create a short LinkedIn post including:

- Your GitHub fork URL
- A 3–5 line explanation of what you contributed and what you learned
- One screenshot of your successfully created Pull Request

## Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/muneer-ahmed-25322b206_devops-git-github-activity-7488111782096650241-30IC?utm_source=share&utm_medium=member_desktop&rcm=ACoAADRb5Z8BfmU5GnTuVjG5eHP-d8cMT-AYl0c

#### Screenshot — LinkedIn post showing the successfully created Pull Request

<img width="672" height="927" alt="image" src="https://github.com/user-attachments/assets/90794181-fab1-4537-9955-4d39706f0161" />


# Submission Instructions

- Add Screenshots 1–9 in the correct task sections
- Add your fork URL and successfully created Pull Request URL
- Show that `origin` points to your fork and `upstream` points to the original repository
- Add the mandatory LinkedIn post URL and screenshot
- Never expose a Personal Access Token, SSH private key, password, recovery code, or authentication secret

---

# Completion Checklist

- [x] Upstream repository forked to your GitHub account
- [x] GitHub authentication configured securely
- [x] Your fork cloned locally
- [x] `origin` points to your fork
- [x] `upstream` points to `pravinmishraaws/devops-micro-internship-interviews`
- [x] `feature-readme-update` created and used
- [x] Only `pull_request.md` modified
- [x] Your entry added at the end of the Student List
- [x] Required commit message used
- [x] Local `main` synchronized with `upstream/main`
- [x] Feature branch rebased and pushed to `origin`
- [x] Pull Request targets the correct upstream repository and `main` branch
- [x] Screenshots 1–9 included and readable
- [x] Mandatory LinkedIn post completed and linked
- [x] No PAT, password, private key, or authentication secret exposed

---

# About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory), focused on real-world execution, systems thinking, and agentic AI workflows.

It helps learners build strong DevOps foundations through hands-on experience.

---

# Resources

* 🌐 DMI Official Website: [https://pravinmishra.com/dmi](https://pravinmishra.com/dmi)
* 🎓 DevOps for Beginners (Udemy): [https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/](https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/)
* 🎓 Agentic AI DevOps with Claude Code: [https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/](https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/)
* 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: [https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/](https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/)
* ▶️ YouTube Playlist: [https://www.youtube.com/playlist?list=PLFeSNDtI4Cho](https://www.youtube.com/playlist?list=PLFeSNDtI4Cho)
* 🔗 Pravin Mishra (LinkedIn): [https://www.linkedin.com/in/pravin-mishra-aws-trainer/](https://www.linkedin.com/in/pravin-mishra-aws-trainer/)
* 🏢 CloudAdvisory (LinkedIn): [https://www.linkedin.com/company/thecloudadvisory/](https://www.linkedin.com/company/thecloudadvisory/)

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
