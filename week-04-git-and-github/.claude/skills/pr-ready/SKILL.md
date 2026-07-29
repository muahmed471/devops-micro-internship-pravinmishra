me: pr-ready
description: Reviews staged Git changes and drafts a PR title, description, and risk report. Never commits, pushes, or opens PRs.
allowed-tools: Bash, Read, Grep
disable-model-invocation: true
---

You are reviewing staged changes before a Pull Request is opened.

1. Run `git diff --cached` and `git status` to see exactly what is staged.
2. Report any of the following if present:
   - secrets or credential-shaped strings
   - debug print/echo statements
   - TODO/FIXME left in code
   - a diff that mixes unrelated concerns
   - a change with no corresponding notes
3. Draft a PR title beginning with a short prefix such as `feat:` or `fix:`, and write a 3–5 sentence PR description explaining what changed and why.
4. Never run `git commit`, `git push`, or `gh pr create`. Never edit files.
   Your output is only a draft for a human to review and use.

Run it with `/pr-ready`.
Screenshot 5

Open SKILL.md in VS Code so the frontmatter is visible, especially:

allowed-tools: Bash, Read, Grep
disable-model-invocation: true

Take the screenshot.

Answers for the Notes
1. Why does /pr-ready have Bash and Read but not Write?

/pr-ready is designed only to inspect the repository and generate a draft Pull Request report. It uses Bash to run Git commands and Read to inspect files, but it does not have Write permissions because it must never modify files, create commits, push changes, or open Pull Requests automatically. Keeping it read-only ensures that a human reviews and approves any changes before they are applied.

2. The pre-commit hook and /pr-ready both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?

Both examined the staged changes, but they served different purposes. The pre-commit hook enforced fixed rules and automatically blocked commits containing known secret patterns or oversized files. The /pr-ready skill performed a broader review by identifying issues such as debug statements, TODO/FIXME comments, mixed or unrelated changes, missing documentation, and drafting a Pull Request title and description. The hook acts as an automated gatekeeper, while the AI skill provides contextual analysis and recommendations.

For Task 5

After removing the fake secret and any debug statements:

git add .
git commit -m "Remove fake secret and debug statements"

Take:

Screenshot 7 → Successful commit.
Screenshot 8 → Clean /pr-ready report.
Task 6 Answers
1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?

I reviewed the AI-generated draft and refined the wording to accurately describe my actual changes. I removed any unnecessary or generic text, ensured the description matched the implemented work, and made it concise and relevant to the Pull Request.

2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?

The draft could contain incorrect assumptions, omit important details, or include inaccurate descriptions of the changes. Submitting it without review could confuse reviewers, misrepresent the work, or reduce the quality and credibility of the Pull Request.

3. Why does this PR need to target your own fork instead of the shared upstream repository?

This assignment is intended for individual practice. Opening the Pull Request against my own fork keeps the experimental hook and AI skill changes separate from the shared upstream repository, preventing unnecessary changes from affecting other contributors.

Task 7 Answers
1. Which step(s) represent Gather?

Gather includes running git status, git diff --cached, and reading the staged files to collect information about the pending changes.

2. Which step(s) represent Analyze?

Analyze includes the pre-commit hook scanning for secret patterns and oversized files, and the /pr-ready skill reviewing the staged changes for risks, debug statements, TODOs, mixed concerns, and preparing a draft Pull Request.

3. Which step is Human Act, and why must a human—not Claude—run git commit, git push, and open the PR?

The Human Act step is reviewing the findings, fixing any issues, running git commit, git push, and creating the Pull Request. These actions permanently modify the repository and should always require human approval to maintain accountability and prevent unintended changes.

4. Which step is Verify?

Verify includes rerunning the pre-commit hook, executing /pr-ready again to confirm no issues remain, ensuring the commit succeeds, and verifying that the Pull Request contains the expected changes.

5. Why do you need both the fixed-rule pre-commit hook and the AI skill? Isn't one enough?

Both tools complement each other. The pre-commit hook provides fast, consistent enforcement of predefined rules, such as blocking known secret patterns and oversized files. The AI skill performs contextual analysis by identifying broader code quality concerns and generating a helpful Pull Request draft. Using both provides stronger protection and a more thorough review than either approach alone.
cl