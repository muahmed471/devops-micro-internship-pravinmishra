<<<<<<< HEAD
<<<<<<< HEAD
# Assignment 3 — CodeTrack Branching Workflow: Contact Page
=======
# Assignment 3 — CodeTrack: Branching Workflow (Add & Verify a Contact Page)
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
# Assignment 3 — CodeTrack: Branching Workflow (Add & Verify a Contact Page)
>>>>>>> upstream/main

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

<<<<<<< HEAD
<<<<<<< HEAD
In this assignment, you will create a feature branch, add a Contact page through two atomic commits, prove that the default branch remains unchanged before merging, merge the feature, and inspect the Git history.
=======
In this assignment, you will add a new Contact page to CodeTrack using a clean feature-branch workflow. You will keep each change in a separate commit, prove that your default branch remains unchanged before the merge, and validate the result after merging.
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
In this assignment, you will add a new Contact page to CodeTrack using a clean feature-branch workflow. You will keep each change in a separate commit, prove that your default branch remains unchanged before the merge, and validate the result after merging.
>>>>>>> upstream/main

---

# Task 1 — Confirm Repository State and Default Branch

## Goal

<<<<<<< HEAD
<<<<<<< HEAD
Start from a clean default branch and confirm that you are working in the correct repository.

### Evidence

#### Screenshot 1 — Output of `git status` and `git branch` showing a clean status and that you are on `main` or `master`
=======
=======
>>>>>>> upstream/main
Start from a clean default branch (`main` or `master`) and confirm the repository status.

### Evidence

#### Screenshot 1 — Output of `git status` and `git branch` showing a clean status and the default branch checked out
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

Add your screenshot here.

---

# Task 2 — Create and Switch to a Feature Branch

## Goal

Create a branch named exactly `feature/contact-page` and switch to it.

### Evidence

<<<<<<< HEAD
<<<<<<< HEAD
#### Screenshot 2 — Branch creation output and `git branch` showing `* feature/contact-page`
=======
#### Screenshot 2 — Output of `git checkout -b feature/contact-page` and `git branch` showing `* feature/contact-page`
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
#### Screenshot 2 — Output of `git checkout -b feature/contact-page` and `git branch` showing `* feature/contact-page`
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
<<<<<<< HEAD
# Task 3 — Add `contact.html` on the Feature Branch

## Goal

Create `contact.html` and record it as a dedicated atomic commit on `feature/contact-page`.
=======
=======
>>>>>>> upstream/main
# Task 3 — Add contact.html on the Feature Branch

## Goal

Create `contact.html` with the provided content and commit it alone using the message `feat(contact): add Contact page`.
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

### Evidence

#### Screenshot 3 — Output of `ls` showing `contact.html`

Add your screenshot here.

---

<<<<<<< HEAD
<<<<<<< HEAD
#### Screenshot 4 — Output of `git commit -m "feat(contact): add Contact page"`
=======
#### Screenshot 4 — Output of `git commit`
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
#### Screenshot 4 — Output of `git commit`
>>>>>>> upstream/main

Add your screenshot here.

---

#### Screenshot 5 — Output of `git log --oneline -3` showing the new commit

Add your screenshot here.

---

<<<<<<< HEAD
<<<<<<< HEAD
# Task 4 — Add the Contact Link to `index.html`

## Goal

Add the Contact page link to the homepage and record it in a separate atomic commit.
=======
=======
>>>>>>> upstream/main
# Task 4 — Add the Contact Link to index.html

## Goal

Add the provided Contact Page link to `index.html` and commit it separately using the message `feat(nav): add Contact Page link`.
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

### Evidence

#### Screenshot 6 — Output of `git status` showing `index.html` as modified before staging

Add your screenshot here.

---

<<<<<<< HEAD
<<<<<<< HEAD
#### Screenshot 7 — Output of `git commit -m "feat(nav): add Contact Page link"`
=======
#### Screenshot 7 — Output of `git commit`
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
#### Screenshot 7 — Output of `git commit`
>>>>>>> upstream/main

Add your screenshot here.

---

#### Screenshot 8 — Browser showing the Contact Page link on the homepage while on `feature/contact-page`

Add your screenshot here.

---

# Task 5 — Verify Isolation (Prove the Default Branch Is Unchanged)

## Goal

<<<<<<< HEAD
<<<<<<< HEAD
Demonstrate that the feature work does not affect `main` or `master` before it is merged.

### Evidence

#### Screenshot 9 — Terminal showing the checkout command and `ls`, proving that `contact.html` is absent
=======
=======
>>>>>>> upstream/main
Switch back to the default branch and confirm that `contact.html` and the Contact Page link do not exist there yet.

### Evidence

#### Screenshot 9 — Terminal showing the checkout and `ls` output, proving `contact.html` is absent
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
<<<<<<< HEAD
#### Screenshot 10 — Browser showing that the Contact Page link is not present on the default branch
=======
#### Screenshot 10 — Browser showing the homepage on the default branch with no Contact Page link
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
#### Screenshot 10 — Browser showing the homepage on the default branch with no Contact Page link
>>>>>>> upstream/main

Add your screenshot here.

---

# Task 6 — Merge the Feature Branch into the Default Branch

## Goal

<<<<<<< HEAD
<<<<<<< HEAD
Merge `feature/contact-page` into `main` or `master` and validate the completed feature.
=======
Merge `feature/contact-page` into your default branch and confirm the Contact page works.
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
Merge `feature/contact-page` into your default branch and confirm the Contact page works.
>>>>>>> upstream/main

### Evidence

#### Screenshot 11 — Output of `git merge feature/contact-page`

Add your screenshot here.

---

#### Screenshot 12 — Output of `ls` showing `contact.html` after the merge

Add your screenshot here.

---

#### Screenshot 13 — Browser showing the Contact page opened from the homepage link on the default branch

Add your screenshot here.

---

# Task 7 — Inspect History (Graph View)

## Goal

<<<<<<< HEAD
<<<<<<< HEAD
Display the repository history in graph form and verify the feature commits.
=======
Display the repository history as a graph and locate both feature commits.
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
Display the repository history as a graph and locate both feature commits.
>>>>>>> upstream/main

### Evidence

#### Screenshot 14 — Full output of `git log --oneline --graph --decorate --all`

Add your screenshot here.

---

# Task 8 — Optional Cleanup (Delete the Feature Branch)

## Goal

<<<<<<< HEAD
<<<<<<< HEAD
Remove the merged local feature branch to keep the branch list clean.

### Optional Evidence

#### Screenshot 15 (Optional) — Output of `git branch -d feature/contact-page` and `git branch` showing successful branch deletion

Add your screenshot here if you complete this task.
=======
=======
>>>>>>> upstream/main
Delete the merged `feature/contact-page` branch to keep your branch list clean.

### Evidence

#### Screenshot 15 (Optional) — Output showing `feature/contact-page` deleted and no longer listed

Add your screenshot here.
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

---

# Submission Instructions

<<<<<<< HEAD
<<<<<<< HEAD
- Add Screenshots 1–14 in the correct task sections
- Add optional Screenshot 15 only if you complete Task 8
- Show that `feature/contact-page` was used for both feature commits
- Show that `contact.html` and the homepage link were absent before merging
- Show that the Contact page works after merging
- Include the graph log showing the relevant commit history
- Do not expose sensitive information
=======
=======
>>>>>>> upstream/main
- Tasks 1–7 are required; Task 8 is optional
- Add all required screenshots in your submission
- Evidence must show `contact.html` and the homepage link were absent before merging, and working after merging
- Do not expose passwords, access tokens, or private keys
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

---

# Completion Checklist

<<<<<<< HEAD
<<<<<<< HEAD
- [ ] Started from a clean `main` or `master` branch
- [ ] Created and used `feature/contact-page`
- [ ] Added `contact.html` with the exact required content
- [ ] Created the atomic Contact page commit
- [ ] Added the Contact Page link to `index.html`
- [ ] Created the separate atomic navigation commit
- [ ] Verified that the default branch was unchanged before merging
- [ ] Merged `feature/contact-page` successfully
- [ ] Verified that `contact.html` exists after merging
- [ ] Verified that the Contact Page link opens correctly
- [ ] Graph history inspected and captured
- [ ] Screenshots 1–14 included and readable
=======
=======
>>>>>>> upstream/main
- [ ] Repository confirmed clean on the default branch (Screenshot 1)
- [ ] `feature/contact-page` created and checked out (Screenshot 2)
- [ ] `contact.html` added in its own commit (Screenshots 3–5)
- [ ] Homepage Contact link added in a separate commit (Screenshots 6–8)
- [ ] Default branch proven unchanged before merge (Screenshots 9–10)
- [ ] Feature branch merged and Contact page verified (Screenshots 11–13)
- [ ] Graph history reviewed (Screenshot 14)
- [ ] Optional cleanup completed (Screenshot 15)
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main
- [ ] No sensitive data exposed

---

<<<<<<< HEAD
<<<<<<< HEAD
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
=======
=======
>>>>>>> upstream/main
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
<<<<<<< HEAD
>>>>>>> b5cecb5 (Split week-04 GitHub assignment into per-topic files, add AI safety-net assignment)
=======
>>>>>>> upstream/main

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
