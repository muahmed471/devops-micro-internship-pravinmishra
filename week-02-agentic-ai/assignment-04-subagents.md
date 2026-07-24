# Assignment 4 — Building Your AI Team

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build and configure a set of specialized AI subagents inside your project. You will learn how different models and tool permissions define agent behavior, and you will trigger two real agent delegations to analyze security and cost aspects of your Terraform infrastructure.

---

# Task 1 — Create the Agents Folder and Add Files

## Goal

Create the `.claude/agents/` directory and add all required agent files.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/agents/` with all 3 files

<<<<<<< HEAD
<img width="295" height="201" alt="image" src="https://github.com/user-attachments/assets/6845a2fe-2d1f-4216-98c7-84b3d98ca504" />

=======
Add your screenshot here.

---
>>>>>>> upstream/main

# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?

<<<<<<< HEAD
Three reasons converge on Haiku for that one agent specifically:

1. The task is pattern-matching, not judgment. Look at its checklist in cost-optimizer.md:16-22 — CloudFront price class tiers, S3 storage class, TTL values, lifecycle rules. These are closed-form comparisons against known AWS pricing knobs ("is this PriceClass_All when PriceClass_100 would work?"). Compare that to security-auditor's job — judging whether an OIDC trust policy is scoped tightly enough or whether an IAM condition actually enforces least privilege requires more nuanced reasoning about attack surface, not just checklist lookup. Sonnet earns its keep there; it would be overkill here.

2. The failure modes are asymmetric in severity. If cost-optimizer misses a savings opportunity or slightly misjudges "impact: medium vs. low," the consequence is a suboptimal recommendation the user reviews and can take or leave. If security-auditor misses a wildcard IAM permission, that's a real vulnerability shipping to production undetected. The agent with the costlier failure mode gets the more capable model; the one with cheap failure modes doesn't need to pay for it.

3. It's advisory-only and read-only. cost-optimizer produces suggestions (current → recommended → estimated impact), never touches files. Since a human is going to look at the recommendations before acting on any of them, there's a built-in check on Haiku's occasional imprecision — unlike tf-writer, whose output becomes the actual infrastructure with no intermediate review step, which is why that one inherits the strongest available model instead.

So it's really a stakes-matched tiering: generation (highest stakes) → inherit, security judgment (high stakes, needs a reliability floor) → sonnet pinned, cost pattern-matching (low stakes, advisory) → haiku.

#### 2. Why does the security auditor NOT have Write in its tools list?

Because giving it Write would break the entire point of having a separate auditor agent.

1. Separation of duties. security-auditor's job is to independently verify what tf-writer produced (its description literally says "Use proactively after generating or modifying Terraform files" — security-auditor.md:3). If the same agent that writes the IAM policy could also silently patch it, you no longer have an independent check — you have the author grading their own homework. The value of an audit comes from it being a separate, adversarial pass over code it didn't create.

2. It's designed to be read, not trusted blindly. The output format is explicitly a report — **Severity** / **Resource** / **Issue** / **Fix** (security-auditor.md:27-31) — a proposed fix as text, not an applied change. That's a deliberate handoff point: a human (or tf-writer, invoked separately) decides whether to apply the fix. Auto-applying security fixes without review is exactly the kind of thing that turns a subtle misunderstanding into a silent, unreviewed change to production infrastructure config.

3. It composes safely with the rest of the system. Because it's strictly Read, Grep, Glob, it's side-effect-free — which is what lets CLAUDE.md's /infra-audit fork it to run in parallel alongside cost-optimizer (also read-only) against the same terraform/ files with zero risk of file-write races or one agent's "fix" corrupting the file another is mid-read on. If either had Write, parallel forking over shared files would be a genuinely risky pattern instead of a safe one.

4. It matches the permission-scoping pattern in the rest of the repo. CLAUDE.md's safety layers already gate Write-equivalent actions at the hook level (PreToolUse blocks terraform destroy, aws s3 rm). Keeping the auditor read-only is the same least-privilege philosophy applied at the agent-config level instead of the hook level — scope the tool, not just the command.

So the omission isn't a gap — Write is the one tool that would undermine the reason this agent exists as separate from tf-writer in the first place.

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

model: inherit at tf-writer.md:5 ties its capability to whatever the user is already running in the parent session, rather than locking in a fixed tier the way the other two do. Two things make that the right call for this specific agent:

1. Generation quality has no ceiling you'd want to impose in advance. Terraform output is the infrastructure — the IAM policy, the S3/CloudFront config it writes becomes what actually gets applied to AWS. Unlike the two auditors, there's no independent downstream check verifying tf-writer's raw output is correct (the security-auditor and cost-optimizer are the check, but they run after, as separate passes). So generation is the one place you don't want to hardcode a ceiling below what's available — you want it running at whatever the best model the user has access to right now is, since a wrong or subtly-insecure Terraform resource is exactly the kind of mistake the rest of this config's safety layers (hooks, auditor agent) exist to catch after the fact, not prevent up front.

2. It's invoked synchronously, in-line with the user's own session, not as a background/parallel check. security-auditor and cost-optimizer get pinned models precisely because they're designed to run proactively and in parallel (via /infra-audit's fork) — they need a predictable quality/cost floor independent of whatever the user happens to be chatting with, since they may fire off without the user actively steering that invocation. tf-writer, by contrast, is driven directly from commands like /scaffold-terraform in the main flow. If the user has already escalated to a stronger model because the task at hand is gnarly (say, a multi-account OIDC setup), inheriting means tf-writer automatically gets that same reasoning boost for free — the CLAUDE.md author doesn't have to predict in advance how hard future Terraform-writing tasks will be and pick a model tier that might be wrong in either direction.

So the split isn't arbitrary: inherit for the one agent whose output is unchecked-until-later and whose invocation rides along with the user's own conscious model choice; pinned for the two agents whose whole purpose is to be a reliable, cost-predictable, independently-running check — where a stable floor matters more than tracking the session's model.
=======
Add your answer here...

---

#### 2. Why does the security auditor NOT have Write in its tools list?

Add your answer here...

---

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

Add your answer here...

---
>>>>>>> upstream/main

### Evidence

#### Screenshot 2 — `security-auditor.md` frontmatter showing model and tools configuration

<<<<<<< HEAD
<img width="1807" height="682" alt="image" src="https://github.com/user-attachments/assets/aa8e7ea6-9504-4298-9099-929c33b7ca8c" />


#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

<img width="1720" height="827" alt="image" src="https://github.com/user-attachments/assets/36dbafdc-4c8a-411d-a7ce-161c37b10971" />

=======
Add your screenshot here.

---

#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — The delegation message showing Claude launched the security-auditor

<<<<<<< HEAD
<img width="1127" height="212" alt="image" src="https://github.com/user-attachments/assets/1c8d0011-5b57-4ee1-b7e4-fd8a7730c59e" />


#### Screenshot 5 — Security audit report output

<img width="1527" height="867" alt="image" src="https://github.com/user-attachments/assets/0f73b8a7-861e-4519-a1ed-fc40f82ea4bb" />

=======
Add your screenshot here.

---

#### Screenshot 5 — Security audit report output

Add your screenshot here.

---
>>>>>>> upstream/main

# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — The full cost optimization report

<<<<<<< HEAD
<img width="1527" height="867" alt="image" src="https://github.com/user-attachments/assets/709c4009-5261-4b81-8d02-eab43b1dc314" />

=======
Add your screenshot here.

---
>>>>>>> upstream/main

# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your GitHub Repo
- Push final changes to your forked GitHub repository

---

## GitHub Repository URL

Paste your forked repository URL here:

<<<<<<< HEAD
https://github.com/muahmed471/devops-micro-internship-pravinmishra/edit/main/week-02-agentic-ai/assignment-04-subagents.md
=======
`Add your URL here`

---
>>>>>>> upstream/main

# Completion Checklist

- [ ] `.claude/agents/` folder contains all 3 agent files
- [ ] Screenshot 2 shows correct `security-auditor.md` configuration
- [ ] Screenshot 3 shows correct `cost-optimizer.md` configuration
- [ ] All 3 written answers completed 
- [ ] Security auditor executed successfully
- [ ] Cost optimizer executed successfully
- [ ] Security report is visible with findings
- [ ] Cost report is visible with recommendations
- [ ] All required screenshots added
- [ ] GitHub repo updated with agents

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

<<<<<<< HEAD
*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
=======
*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
>>>>>>> upstream/main
