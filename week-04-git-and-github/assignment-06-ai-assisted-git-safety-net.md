
# Assignment 2 — Building an AI-Assisted Git Safety Net (PR Ready Check)
# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---


# Task 1 — Create a Branch with Realistic Risk

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="961" height="157" alt="image" src="https://github.com/user-attachments/assets/4e19141b-7ecd-475b-aa1b-395a8037f409" />


### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A dedicated branch isolates your work from the stable main branch, allowing you to make changes, test them, and submit them for review without affecting the main codebase. It also makes collaboration easier by keeping each feature or fix in its own branch, simplifying code reviews, rebasing, and merge conflict resolution. Once the changes are approved, the branch can be safely merged into main, ensuring the main branch remains clean and stable.

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.


### What to do

```bash
git checkout -b feature/ai-pr-ready
```

Create a file `scripts/notify.sh` (or edit any existing script) that includes a fake AWS-style key and a debug `echo`, for example:

```bash
#!/bin/bash
# demo only — fake credential for this assignment, never a real key
AWS_ACCESS_KEY_ID=AKIAABCDEFGHIJKLMNOP
echo "DEBUG: token is $AWS_ACCESS_KEY_ID"
```

Stage it with `git add`.

### Evidence

#### Screenshot 1 — `git status` showing the staged file on your new branch

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready


<img width="1202" height="281" alt="image" src="https://github.com/user-attachments/assets/f6524a2a-7dfe-47ae-a65f-cefbc7c2d1a7" />


### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

A fake key is used to teach the correct Git workflow without exposing sensitive credentials. Real API keys, SSH keys, or access tokens should never be committed to a Git repository because they can be misused if the repository is public or shared. Using a dummy key allows you to practice handling secrets safely, recognize sensitive data, and learn how to avoid accidentally leaking credentials. This reinforces security best practices while ensuring no real accounts or services are put at risk.

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### What to do

Create `hooks/pre-commit` (tracked in the repo, not `.git/hooks/`, so teammates get it too):

```bash
#!/bin/bash
# hooks/pre-commit — blocks commits with likely secrets or oversized files
set -e

staged=$(git diff --cached --name-only --diff-filter=ACM)
blocked=0

for file in $staged; do
  if git diff --cached -- "$file" | grep -qE 'AKIA[0-9A-Z]{16}|-----BEGIN (RSA|OPENSSH|PRIVATE) KEY-----'; then
    echo "BLOCKED: possible secret in $file"
    blocked=1
  fi
  size=$(git cat-file -s "$(git rev-parse ":$file")" 2>/dev/null || echo 0)
  if [ "$size" -gt 1000000 ]; then
    echo "BLOCKED: $file is $(($size / 1000000))MB — over the 1MB limit"
    blocked=1
  fi
done

if [ "$blocked" -eq 1 ]; then
  echo "Commit rejected. Fix the issues above and try again."
  exit 1
fi
```

Point Git at the tracked hooks folder and make it executable:

```bash
chmod +x hooks/pre-commit
git config core.hooksPath hooks
```
upstream/main
### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="1467" height="742" alt="image" src="https://github.com/user-attachments/assets/7f921797-0f96-4f51-b07a-c01c394531cd" />


#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="1337" height="137" alt="image" src="https://github.com/user-attachments/assets/9b7820af-6fa2-4a1e-9083-b42810b4c9c5" />


### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

hooks/pre-commit is tracked in the repository so the hook can be shared with all contributors and version-controlled along with the project. The .git/hooks/ directory is local to each developer's Git repository and is not committed or shared. By keeping the hook in a tracked hooks/ directory and configuring core.hooksPath, every team member can use the same pre-commit checks, ensuring consistent validation and security across the project.

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

A Git pre-commit hook intercepts a commit before it is recorded in the Git repository. It can block the commit if it detects problems such as secret keys, large files, or formatting issues.

A PreToolUse hook intercepts tool execution in an AI workflow before the tool is allowed to run. It can validate, restrict, or deny the requested action based on predefined rules.

Both act as preventive gatekeepers. They perform validation before an action is executed, enforce policies automatically, and stop unsafe or invalid operations before they can cause problems. The difference is that a Git pre-commit hook protects the source code repository, while a PreToolUse hook protects AI tool execution and system interactions.

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="1151" height="195" alt="image" src="https://github.com/user-attachments/assets/63c29901-eeda-4505-8396-79b9739ffe0e" />


### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

It matched because the fake key used the AWS Access Key ID pattern, which starts with AKIA followed by 16 uppercase letters or numbers. The grep -E command uses this regular expression to detect strings that resemble AWS access keys or private key headers and blocks the commit if a match is found.

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

No. This hook only detects secrets that match the specific patterns defined in its regular expression, such as AWS access keys beginning with AKIA or private key headers. If a secret were stored in a variable with a different format or a custom token that doesn't match these patterns, the hook would not detect it. This demonstrates the limitation of fixed rule-based detection: it is effective for known patterns but cannot identify every possible secret. In real-world projects, teams often combine pattern-based scanning with entropy-based detection and dedicated secret-scanning tools such as GitHub Secret Scanning, Gitleaks, or TruffleHog for more comprehensive protection.

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.


### What to do

Create `.claude/skills/pr-ready/SKILL.md` with frontmatter restricting it to read-only inspection tools:

```markdown
---
name: pr-ready
description: Reviews staged Git changes and drafts a PR title, description, and risk report. Never commits, pushes, or opens PRs.
allowed-tools: Bash, Read, Grep
disable-model-invocation: true
---

You are reviewing staged changes before a Pull Request is opened.

1. Run `git diff --cached` and `git status` to see exactly what is staged.
2. Report any of the following if present: secrets or credential-shaped
   strings, debug print/echo statements, TODO/FIXME left in code, a diff
   that mixes unrelated concerns, or a change with no corresponding notes.
3. Draft a PR title that starts with a short word like `feat:` or `fix:`
   telling the reader what kind of change this is, and a 3-5 sentence PR
   description explaining what changed and why.
4. Never run `git commit`, `git push`, or `gh pr create`. Never edit files.
   Your output is a draft for a human to review and use.
```

Run it with `/pr-ready`.


### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img width="1702" height="911" alt="image" src="https://github.com/user-attachments/assets/a7960c00-88d2-43c8-9d3f-f41f8f33c79e" />


#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

<img width="1772" height="695" alt="image" src="https://github.com/user-attachments/assets/a7bc921f-6b7f-4f65-9f84-900b086970e6" />


### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

/pr-ready is designed only to inspect the repository and generate a draft Pull Request report. It uses Bash to run Git commands and Read to inspect files, but it does not have Write permissions because it must never modify files, create commits, push changes, or open Pull Requests automatically. Keeping it read-only ensures that a human reviews and approves any changes before they are applied.

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both examined the staged changes, but they served different purposes. The pre-commit hook enforced fixed rules and automatically blocked commits containing known secret patterns or oversized files. The /pr-ready skill performed a broader review by identifying issues such as debug statements, TODO/FIXME comments, mixed or unrelated changes, missing documentation, and drafting a Pull Request title and description. The hook acts as an automated gatekeeper, while the AI skill provides contextual analysis and recommendations.

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img width="1482" height="157" alt="image" src="https://github.com/user-attachments/assets/490b68b1-fdaa-4839-b8bf-1e5114c6d230" />


#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img width="907" height="222" alt="image" src="https://github.com/user-attachments/assets/d3fbbae3-5dd7-4d30-84ce-6cb9c43125d8" />


### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the fake AWS access key and any debug statements from the staged files, then staged the corrected changes again. This ensured that the pre-commit hook no longer detected any secret-like patterns or blocked content, allowing the commit to complete successfully.

# Task 6 — Open the Pull Request Using the AI Draft

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

<img width="1872" height="1082" alt="image" src="https://github.com/user-attachments/assets/4a5189de-f694-43dd-bf2a-286f112fcfc5" />


#### PR Link

https://github.com/pravinmishraaws/devops-micro-internship-interviews/pull/435

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I reviewed the AI-generated draft and updated it to accurately reflect my actual changes. I removed any generic wording, ensured the description matched the work completed, and made it clearer and more concise so reviewers would understand the purpose and scope of the Pull Request.

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The AI draft could contain incorrect assumptions, omit important details, or describe changes that were not actually made. Reviewing it before submitting helps ensure the Pull Request is accurate, complete, and provides reviewers with reliable information.

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This assignment is intended for individual practice, so the Pull Request should target my own fork instead of the shared upstream repository. Doing so keeps my experimental changes separate from the main project, prevents unnecessary pull requests to the shared repository, and allows me to safely test the workflow without affecting other contributors.

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

The Gather step includes collecting information about the staged changes by running commands such as git status and git diff --cached. It also involves reading the relevant files to understand exactly what will be included in the commit.

**2. Which step(s) represent Analyze?**

The Analyze step is performed by the pre-commit hook and the /pr-ready skill. The pre-commit hook checks for secret-like patterns and oversized files, while /pr-ready analyzes the staged changes for risks such as debug statements, TODO/FIXME comments, mixed changes, and drafts a Pull Request title and description.

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

The Human Act step is reviewing the AI's recommendations, fixing any identified issues, running git commit, pushing the branch, and creating the Pull Request. These actions permanently change the repository and publish code, so they require human approval and accountability to prevent unintended or incorrect changes.

**4. Which step is Verify?**

The Verify step includes rerunning the pre-commit hook and the /pr-ready skill after making fixes, confirming that the commit succeeds without being blocked, and ensuring the Pull Request accurately reflects the intended changes.

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The pre-commit hook provides fast, consistent enforcement of predefined security and file-size rules, while the AI skill performs a broader contextual review and generates a helpful Pull Request draft. Together, they provide stronger quality assurance than either tool could provide on its own.

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/muneer-ahmed-25322b206_devops-git-githooks-activity-7488132639502270465-EGql?utm_source=share&utm_medium=member_desktop&rcm=ACoAADRb5Z8BfmU5GnTuVjG5eHP-d8cMT-AYl0c

## Key Learnings

Add 3-5 bullet points on what you learned this week.

1. Learned how to create and configure a custom Git pre-commit hook to prevent committing secret-like patterns and oversized files.
2. Understood the difference between fixed-rule validation (Git hooks) and AI-assisted code review using a read-only /pr-ready skill.
3. Practiced creating feature branches, rebasing with upstream changes, and following a professional Pull Request workflow.
4. Improved understanding of secure development practices by validating changes before committing and submitting code.
5. Recognized the importance of reviewing AI-generated suggestions instead of accepting them without verification.

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/muahmed471/devops-micro-internship-interviews/tree/feature/ai-pr-ready

# Completion Checklist

- [x] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [x] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [x] `core.hooksPath` configured to point at `hooks/`
- [x] Pre-commit hook shown blocking the risky commit
- [x] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [x] `/pr-ready` run against the risky diff and shown flagging issues
- [x] Risky file fixed; `git commit` succeeds cleanly
- [x] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [x] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [x] Agentic Loop mapping (Task 7) completed in your own words
- [x] LinkedIn post published and URL submitted
- [x] All required screenshots added
- [x] GitHub repository URL provided

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
