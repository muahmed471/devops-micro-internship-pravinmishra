# Assignment 2 — Building an AI-Assisted Git Safety Net (PR Ready Check)

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

Add your screenshot here.

![screenshot](./screenshots/Assignment06-screenshot1.png)

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

The assignment uses a fake key because it is meant for learning and testing Git/security practices, not for using a real credential.

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

chmod +x hooks/pre-commit
git config core.hooksPath hooks


### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

![screenshot](./screenshots/Assignment06-screenshot2.png)

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

![screenshot](./screenshots/Assignment06-screenshot3.png)

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

hooks/pre-commit is tracked in the repository so that the pre-commit security checks can be shared with the entire team.

The .git/hooks/ directory is local to each developer's machine and is not tracked by Git, so hooks stored there are not automatically shared when someone clones the repository.

By keeping the hook in hooks/pre-commit, everyone gets the same hook when they clone or pull the repository. It also allows the team to version-control changes to the security checks.


**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

PreToolUse and the Git pre-commit hook both act as preventive checkpoints, but they intercept different things.

Git pre-commit hook: Runs when you are about to create a Git commit. It can inspect the staged files and block the commit if it finds things such as secret-like patterns or files larger than 1 MB.
PreToolUse from Week 2 Assignment 6: Runs before an AI agent executes a tool. It can inspect the tool being requested and its arguments, then allow or block the tool call based on predefined rules.
What they have in common: Both are early interception mechanisms. They run before an action is completed, allowing potentially unsafe or unwanted actions to be stopped before they cause a problem.

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

![screeshot](./screenshots/Assignment06-screenshot4.png)

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line that matched the fake key is if git diff --cached -- "$file" | grep -qE 'AKIA[0-9A-Z]{16}|-----BEGIN (RSA|OPENSSH|PRIVATE) KEY-----'; then Specifically, this pattern matched AKIA[0-9A-Z]{16} The fake key was AKIAABCDEFGHIJKLMNOP.

It matched because:

AKIA matches the literal AKIA prefix.
[0-9A-Z]{16} matches exactly 16 uppercase letters or digits following AKIA.
Therefore, the hook recognized the value as an AWS access-key-like pattern and blocked the commit.

In short, grep -qE found the AKIA... pattern in the staged file, causing the hook to set blocked=1 and reject the commit.

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

fixed rules are useful as a first line of defense, but they can produce both false negatives (missed secrets) and potentially false positives (normal text that happens to match a pattern). More advanced secret scanning tools are needed for broader detection.

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

![screeshot](./screenshots/Assignment06-screenshot5.png)

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

Add your screenshot here.

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

/pr-ready is designed to inspect the repository and report whether it is ready for a pull request, not to modify files. Read allows it to examine files, and Bash allows it to run commands such as checking the staged Git diff. It does not need Write because it should not make changes to the working tree. This follows the principle of least privilege: give the command only the permissions it needs.

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

No, they did not necessarily flag the same things. The pre-commit hook used fixed patterns and detected the fake AWS key because it matched the AKIA[0-9A-Z]{16} pattern. /pr-ready performed a broader review and could also flag the debug statement, such as printing the credential with echo.

This shows that the two checks complement each other: the pre-commit hook provides fast, deterministic protection against known patterns, while /pr-ready can apply broader contextual checks to identify risky code that a simple fixed pattern may miss.

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

Add your screenshot here.

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

Add your screenshot here.

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

Add your answer here.

---

# Task 6 — Open the Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

Add your screenshot here.

---

#### PR Link

Add your PR URL here...

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I reviewed the AI-generated PR description and corrected any inaccurate or unclear details, especially the description of the changes and security checks. I did this because AI-generated content can contain assumptions or mistakes, so the final PR description should accurately reflect what was actually changed and tested.

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The PR description could contain incorrect claims, missing information, or misleading statements about the changes and test results. It might say that a security check passed when it did not, or describe files and changes that were never actually made. This could confuse reviewers and reduce trust in the PR.

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

The PR should target my own fork because I do not have direct write access to the shared upstream repository. The fork provides a separate copy where I can safely make changes and push my branch. I can then create a PR from my fork to the upstream repository for review without directly modifying the shared repository.

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

The Gather stage is where information is collected without making changes.

Examples in this assignment include:

The pre-commit hook examining the staged Git diff.
/pr-ready using Read and Bash to inspect the repository and staged changes.
Checking git status and the staged files.
Collecting information about possible secrets, debug statements, and oversized files.

The goal is to collect the relevant repository information before making a decision.

**2. Which step(s) represent Analyze?**

The Analyze stage is where the collected information is evaluated.

In this assignment:

The pre-commit hook analyzes the staged content against fixed secret patterns and the 1 MB file-size rule.
/pr-ready analyzes the staged diff more broadly and identifies potential problems such as secrets or debug statements.
The AI drafts a PR description based on the changes and findings.

This stage helps determine whether the changes are safe and ready for review.

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

The Human Act stage is when I review the results and make the final decision to:

git commit
git push
Open the Pull Request

A human should perform these actions because they are real-world actions that change repository state and can affect other people or shared code.

The AI can inspect the changes, identify risks, and prepare a PR description, but the human should remain responsible for the final decision. This provides a human approval checkpoint before code is committed, pushed, and submitted for review.

**4. Which step is Verify?**

The Verify step is performed after the human commits, pushes, and opens the PR. It involves checking that the commit was created successfully, the correct branch was pushed to my fork, the PR targets the correct upstream repository, and the final PR contains the expected changes.

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

Both provide different layers of protection: the pre-commit hook reliably blocks known patterns such as AWS keys and oversized files, while the AI skill can identify broader, context-dependent issues such as debug statements or suspicious changes. Together, they provide stronger protection than either one alone.

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/muneer-ahmed-25322b206_devops-devsecops-git-activity-7495445757135601664-YfKP?utm_source=share&utm_medium=member_desktop&rcm=ACoAADRb5Z8BfmU5GnTuVjG5eHP-d8cMT-AYl0c

## Key Learnings

Add 3-5 bullet points on what you learned this week.

a) Learned how to build a tracked Git pre-commit hook that blocks secret-like patterns and oversized files before they are committed.
b) Learned the difference between fixed-rule security checks and AI-assisted review, and why both are useful together.
c) Learned how the Gather → Analyze → Human Act → Verify workflow keeps humans responsible for consequential Git and PR actions.
d) Learned that AI-generated PR descriptions and code reviews should always be reviewed and verified by a human before being used.
e) Learned the importance of layered security controls because fixed rules can miss secrets or risky code that doesn't match predefined patterns.

---

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

`Add your URL here`

---

# Completion Checklist

- [x] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [x] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [x] `core.hooksPath` configured to point at `hooks/`
- [] Pre-commit hook shown blocking the risky commit
- [x] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [x] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

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
