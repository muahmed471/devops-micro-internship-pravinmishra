# Assignment 2 — Tracking, Staging, Committing + Deploy to EC2 (CodeTrack)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will track and stage project files, create two meaningful Git commits, verify the repository history, and deploy the CodeTrack static website to an EC2 web server using Nginx.

---

# Task 1 — Verify Git Setup and Enter the Repository

## Goal

Confirm that Git works and that you are inside the correct CodeTrack repository.

### Evidence

#### Screenshot 1 — Output of `pwd`

<img width="617" height="61" alt="image" src="https://github.com/user-attachments/assets/d1955c45-6729-4f10-ab3d-4616ce06b6c1" />

#### Screenshot 2 — Output of `git status`

<img width="602" height="145" alt="image" src="https://github.com/user-attachments/assets/12d57a43-ddcc-4658-bac0-bf82e287b64e" />


# Task 2 — Create `index.html` and `style.css`

## Goal

Create the two starter UI files and confirm that both files exist.

### Evidence

#### Screenshot 3 — Commands and output showing `index.html` and `style.css` in the directory listing

<img width="635" height="56" alt="image" src="https://github.com/user-attachments/assets/e5e208d9-b746-4cbc-90cc-6ed6440d1201" />


# Task 3 — Add Starter Content

## Goal

Add the provided starter HTML and CSS content to the local CodeTrack files.

### Evidence

#### Screenshot 4 — Your editor showing the contents of `index.html` and `style.css`; one screenshot is acceptable if both files are visible

<img width="1657" height="1087" alt="image" src="https://github.com/user-attachments/assets/368bb93d-9701-40cd-b8e8-410e8f0bdcb5" />
<img width="1187" height="1100" alt="image" src="https://github.com/user-attachments/assets/ffae4a8f-9ec9-4fba-8085-039125991593" />


# Task 4 — Track and Stage Files Correctly

## Goal

Identify the untracked files, stage them intentionally, and verify the staging area.

### Evidence

#### Screenshot 5 — Output of `git status` showing both files as untracked

<img width="762" height="222" alt="image" src="https://github.com/user-attachments/assets/8596c5f9-4580-4bcd-84d7-54b8432b2021" />


#### Screenshot 6 — Output of `git status` showing both files staged under Changes to be committed

<img width="762" height="225" alt="image" src="https://github.com/user-attachments/assets/6d1ca6dc-2f33-4cb5-9028-b77611b5c647" />


# Task 5 — Create the First Commit (Clean Initial Commit)

## Goal

Create the first commit with the required meaningful message and verify the repository history.

### Evidence

#### Screenshot 7 — Output of `git commit -m "Initial UI scaffold: add index.html and style.css"`

<img width="792" height="117" alt="image" src="https://github.com/user-attachments/assets/4ee42d7e-207d-43ff-a6af-fae59f293275" />


#### Screenshot 8 — Output of `git log --oneline` showing the first commit

<img width="701" height="71" alt="image" src="https://github.com/user-attachments/assets/58703c95-6716-4ced-870d-eb7f61354222" />


# Task 6 — Modify `index.html` and Create a Second Commit

## Goal

Complete a controlled homepage change and record it as a separate, meaningful commit.

### Evidence

#### Screenshot 9 — Browser showing the updated page with visible Student Name and Group Name changes

<img width="1595" height="1092" alt="image" src="https://github.com/user-attachments/assets/c1d2dd96-cae4-41bc-976c-0d694e7e9e83" />


#### Screenshot 10 — Output of `git status` showing `index.html` as modified

<img width="717" height="197" alt="image" src="https://github.com/user-attachments/assets/c2872e73-7687-454e-aee7-0f9c2f0ca9e2" />


#### Screenshot 11 — Output of `git commit -m "Update homepage content: heading, tagline, CTA button"`

<img width="695" height="117" alt="image" src="https://github.com/user-attachments/assets/7432fc3c-5d73-4c46-9381-a1a3cadea85b" />


#### Screenshot 12 — Output of `git log --oneline` showing two commits

Add your screenshot here.

---

# Task 7 — Deploy to EC2 with Nginx (Static Website)

## Goal

Deploy the CodeTrack static website to a live Ubuntu or Amazon Linux EC2 instance using Nginx.

### Evidence

#### Screenshot 13 — Nginx status output showing `active (running)`

Add your screenshot here.

---

#### Screenshot 14 — Output of `curl -I http://localhost` showing `HTTP 200 OK`

Add your screenshot here.

---

#### Screenshot 15 — Browser showing the CodeTrack site loaded from `http://<EC2_PUBLIC_IP>`, with the URL, Full Name, and Group Name visible

Add your screenshot here.

---

# Live Application URL

Paste your live CodeTrack application URL here:

`Add your URL here`

---

# LinkedIn Post (Mandatory)

Your post must include:

- Your live CodeTrack application URL
- A 3–5 line explanation of what you deployed and what you learned
- One screenshot of the deployed application showing your Full Name

## Evidence

#### LinkedIn Post URL

`Add your URL here`

---

#### Screenshot — LinkedIn post showing the deployed application

Add your screenshot here.

---

# Submission Instructions

- Add all 15 required screenshots in the correct task sections
- Include `git log --oneline` output showing at least two meaningful commits
- Add the live CodeTrack application URL
- Add the required LinkedIn post URL and screenshot
- Do not expose AWS keys, passwords, private key contents, or other sensitive information

---

# Completion Checklist

- [x] CodeTrack repository verified with `git status`
- [x] `index.html` and `style.css` created and populated
- [x] Starter files staged and committed in the first commit
- [x] Student Name and Group Name updated in `index.html`
- [x] Second controlled commit created
- [x] `git log --oneline` shows at least two commits
- [x] Nginx is active on the EC2 instance
- [x] `curl` returns HTTP 200 OK
- [x] CodeTrack loads through the EC2 public IP
- [x] All 15 required screenshots included
- [x] Mandatory LinkedIn post completed and linked
- [x] No sensitive data exposed

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
