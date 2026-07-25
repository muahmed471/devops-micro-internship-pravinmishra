# Assignment 2 — CodeTrack: Tracking, Staging, Committing + Deploy to EC2

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will track and stage project files, create two meaningful Git commits in `CodeTrack`, verify your commit history, and deploy the CodeTrack static website to an EC2 instance using Nginx. This connects local version-control practice with a basic manual deployment workflow used in real DevOps environments.

---

# Task 1 — Verify Git Setup and Enter the Repository

## Goal

Confirm that Git works and that you are inside the correct `CodeTrack` repository.

### Evidence

#### Screenshot 1 — Output of `pwd` showing you're inside `CodeTrack`

<img width="605" height="121" alt="image" src="https://github.com/user-attachments/assets/ba3e285a-3249-4f37-abe7-9da7b4d0c03f" />


#### Screenshot 2 — Output of `git status` showing no "not a git repository" error

<img width="635" height="177" alt="image" src="https://github.com/user-attachments/assets/e30a0447-70d7-4754-99d1-48f514ce5c2d" />


# Task 2 — Create index.html and style.css

## Goal

Create the two starter UI files inside `CodeTrack`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `index.html` and `style.css`

<img width="607" height="107" alt="image" src="https://github.com/user-attachments/assets/c5535add-c3ba-432b-94d9-773d4deb2251" />


# Task 3 — Add Starter Content

## Goal

Copy the provided starter HTML and CSS content into your local `index.html` and `style.css` files.

### Evidence

#### Screenshot 4 — Your editor showing the contents of `index.html` and `style.css`

<img width="1631" height="861" alt="image" src="https://github.com/user-attachments/assets/aa3001c4-91bf-469a-bd91-369a1c517342" />
<img width="1877" height="846" alt="image" src="https://github.com/user-attachments/assets/a9f253e7-637a-4086-bd21-356ea56f3c92" />


# Task 4 — Track and Stage Files Correctly

## Goal

Confirm both files show as untracked, then stage them individually with `git add`.

### Evidence

#### Screenshot 5 — Output of `git status` showing both files as untracked

<img width="730" height="261" alt="image" src="https://github.com/user-attachments/assets/452c12cf-4d36-49f4-ac12-613075183c07" />


#### Screenshot 6 — Output of `git status` showing both files staged under "Changes to be committed"

<img width="670" height="242" alt="image" src="https://github.com/user-attachments/assets/967cda79-81e8-47a6-9379-37f2f0f4db44" />


# Task 5 — Create the First Commit (Clean Initial Commit)

## Goal

Commit the staged starter files using the message `Initial UI scaffold: add index.html and style.css`, then check the log.

### Evidence

#### Screenshot 7 — Output of `git commit`

<img width="757" height="122" alt="image" src="https://github.com/user-attachments/assets/f6ba8693-6bf2-4e9d-b197-881d7d402c6c" />


#### Screenshot 8 — Output of `git log --oneline` showing the first commit

<img width="677" height="87" alt="image" src="https://github.com/user-attachments/assets/599f1010-bc1d-4e0d-b41b-7410ec23d1df" />


# Task 6 — Modify index.html and Create a Second Commit

## Goal

Follow the instruction comment inside `index.html` to update the Student Name and Group Name, then commit that change separately using the message `Update homepage content: heading, tagline, CTA button`.

### Evidence

#### Screenshot 9 — Browser showing the updated page with your Student Name and Group Name visible

<img width="1731" height="837" alt="image" src="https://github.com/user-attachments/assets/71ec24fb-52da-474b-b7b0-051fe4d59506" />


#### Screenshot 10 — Output of `git status` showing `index.html` as modified

<img width="642" height="217" alt="image" src="https://github.com/user-attachments/assets/d3fd6171-356b-4b78-afae-2babdcaf3de6" />


#### Screenshot 11 — Output of `git commit`

<img width="936" height="347" alt="image" src="https://github.com/user-attachments/assets/85da5eb4-aa01-4e47-80aa-31c623816649" />


#### Screenshot 12 — Output of `git log --oneline` showing two commits

<img width="732" height="121" alt="image" src="https://github.com/user-attachments/assets/d746388a-928b-4dbb-9e0a-476aa057c19c" />


# Task 7 — Deploy to EC2 with Nginx (Static Website)

## Goal

Install and start Nginx on your EC2 instance, then copy `index.html` and `style.css` into the Nginx web root.

### Evidence

<<<<<<< HEAD
#### Screenshot 13 — Output showing Nginx `active (running)`
=======
#### Screenshot 13 — Output of `systemctl status nginx --no-pager` showing Nginx `active (running)`
>>>>>>> upstream/main

<img width="1436" height="395" alt="image" src="https://github.com/user-attachments/assets/66b59450-45ca-4e23-881b-7af68f3d5ad7" />


#### Screenshot 14 — Output of `curl -I http://localhost` showing `HTTP/1.1 200 OK`

<img width="847" height="215" alt="image" src="https://github.com/user-attachments/assets/625183d0-cab7-4e1a-a0f9-a404960e7d03" />


#### Screenshot 15 — Browser showing the CodeTrack site loaded at `http://<EC2_PUBLIC_IP>`, with your Full Name and Group Name visible

<img width="1716" height="867" alt="image" src="https://github.com/user-attachments/assets/5648b179-1fbe-4195-894b-38e6d43b4ec1" />


# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/muneer-ahmed-25322b206_dmibypravinmishra-devops-nginx-activity-7486731133720915969-RwMZ?utm_source=share&utm_medium=member_desktop&rcm=ACoAADRb5Z8BfmU5GnTuVjG5eHP-d8cMT-AYl0c

#### Screenshot — LinkedIn post showing the deployed CodeTrack application

<img width="675" height="917" alt="image" src="https://github.com/user-attachments/assets/22718f0a-33e6-42f3-af3c-fff398c2d329" />


# Submission Instructions

- Add all required screenshots in your submission
- Full Name and Group Name must be visible in the deployed application evidence
- `git log --oneline` output must show at least two meaningful commits
- Do not expose AWS access keys, passwords, private key contents, or other sensitive information

---

# Completion Checklist

- [ ] `CodeTrack` repository verified with `git status` (Screenshots 1–2)
- [ ] `index.html` and `style.css` created and populated (Screenshots 3–4)
- [ ] Starter files staged and committed in the first commit (Screenshots 5–8)
- [ ] Student Name and Group Name updated in `index.html` (Screenshot 9)
- [ ] Second controlled commit created (Screenshots 10–12)
- [ ] Nginx active on the EC2 instance and CodeTrack reachable via its public IP (Screenshots 13–15)
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

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
