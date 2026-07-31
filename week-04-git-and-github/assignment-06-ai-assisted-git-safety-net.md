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

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="1022" height="262" alt="image" src="https://github.com/user-attachments/assets/23b75b48-c3a3-4535-bfe9-90106c8c4bc8" />


---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A dedicated branch keeps unfinished assignment work separate from the stable main branch. It also makes the changes easier to review, test, modify, and merge through a Pull Request without affecting completed work.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

<img width="990" height="142" alt="image" src="https://github.com/user-attachments/assets/2a6e4d34-2aab-4560-9b82-3b5ead1a7395" />


---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

A real secret must never be placed in source code, Git history, screenshots, or assignment submissions. A fake key safely tests whether the security rule works without exposing credentials or creating a security incident.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="1447" height="667" alt="image" src="https://github.com/user-attachments/assets/f72138d6-8850-4257-866c-e060b65d29b6" />


---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="937" height="90" alt="image" src="https://github.com/user-attachments/assets/3f1ebb6b-eac5-4c26-ad95-f0e279b93947" />


---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Files inside .git/hooks/ are local to one repository copy and are not committed or shared. Keeping the hook in a tracked hooks directory allows every team member to receive the same script when they clone or pull the repository. Each person only needs to configure core.hooksPath.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

A Git pre-commit hook intercepts a commit before Git creates it. It checks staged repository content using fixed rules.

Claude Code’s PreToolUse hook intercepts an AI tool action before Claude executes that tool.

Both act as preventive controls: they inspect an intended action before it happens and can block it when predefined safety conditions are violated.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="907" height="106" alt="image" src="https://github.com/user-attachments/assets/dbe90817-ba12-4870-afd8-ba0cf71afe82" />

---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

const awsAccessKey = "AKIA1234567890ABCDEF";

It matched the hook pattern:

AKIA[0-9A-Z]{16}

The value begins with AKIA and is followed by exactly 16 uppercase letters or numbers, which resembles the structure of an AWS access key ID.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

Not necessarily. This hook only detects values that match the specific patterns defined in the script. A secret with an unfamiliar format, an encoded value, or a normal-looking variable name could bypass it. This shows that fixed rules are consistent and useful, but they cannot understand context or detect every possible security risk. Human review and more advanced secret-scanning tools are still necessary.

---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img width="1466" height="507" alt="image" src="https://github.com/user-attachments/assets/ad38a546-92fc-45f9-956a-d5645cf11a3a" />


---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

<img width="1270" height="830" alt="image" src="https://github.com/user-attachments/assets/c15baa26-6a49-42b5-97f7-f8d28eab4659" />


---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

Bash allows the skill to inspect commands such as git status and git diff --cached, while Read and Grep allow it to examine staged content. Write is intentionally excluded so the skill cannot change files or silently fix, commit, or alter the developer’s work.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both examined the same staged changes and identified the credential-shaped AWS key. The fixed hook blocked the key because it matched a predefined pattern, while /pr-ready could also recognize the leftover debug statement and explain the broader review risk. The hook enforces deterministic rules; the AI skill provides contextual advice.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img width="977" height="122" alt="image" src="https://github.com/user-attachments/assets/16ba819f-eed9-40ca-9f34-a268975b50ba" />


---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img width="1217" height="497" alt="image" src="https://github.com/user-attachments/assets/0eaef97b-40f0-405d-a571-f5d3f61afd23" />


---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the hardcoded fake AWS key and the debug statement that printed the key. The revised script reads the credential from the environment, checks whether it exists, and prints only a safe status message without exposing the credential.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

<img width="1527" height="887" alt="image" src="https://github.com/user-attachments/assets/67be2623-1a81-4b73-aac2-d42046899dbd" />

---

#### PR Link

https://github.com/pravinmishraaws/devops-micro-internship-interviews/pull/449

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I checked the AI-generated description against the actual files and commands used. I corrected or removed any unsupported statements and added the exact validation steps so the PR accurately describes the implementation.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The draft might contain inaccurate claims, omit an important risk, describe files that were not changed, or use the wrong PR scope. AI output is advisory and must be checked against the actual diff.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This assignment is a private workflow exercise and should not send experimental hooks or Claude configuration to the shared upstream repository. Targeting my own fork allows me to demonstrate the PR workflow without affecting or requesting changes from the course repository.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

git status, git diff --cached, file-size checks, pattern scanning, and the skill’s reading of staged files represent the Gather stage. They collect facts about exactly what will be committed.

---

**2. Which step(s) represent Analyze?**

The pre-commit hook analyzes staged content using deterministic patterns and size limits. /pr-ready analyzes the same diff contextually for secrets, debug statements, mixed concerns, missing explanation, and PR clarity.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

The human fixes the files, stages them, runs git commit, pushes the branch, reviews the AI draft, and opens the Pull Request. These actions modify repository history or shared GitHub state, so they must remain under human control rather than being automatically performed by Claude.

---

**4. Which step is Verify?**

Re-running /pr-ready, successfully passing the pre-commit hook, checking git status, reviewing git log, and inspecting the final Pull Request represent Verify.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The fixed hook consistently enforces known rules and can reliably block specific patterns. The AI skill provides contextual review and can identify concerns such as debug output or unclear scope that rigid pattern matching may miss.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

Add your LinkedIn post URL here...

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

-
-
-

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
https://github.com/DMIC3-G1-Anishkumar/devops-micro-internship-interviews.git

---

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
