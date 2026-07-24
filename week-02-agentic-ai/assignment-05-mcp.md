# Assignment 5 — Connecting Claude to the Outside World

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to external systems using MCP (Model Context Protocol). You will configure the GitHub MCP server, securely store credentials, verify the connection, and run a live query that proves Claude is accessing real-time GitHub data.

---

# Task 1 — Create a GitHub Personal Access Token

## Goal

Generate a GitHub Personal Access Token (PAT) that will be used for MCP authentication.

### Evidence

#### Screenshot 1 — GitHub token creation page showing the selected scopes (`repo`, `read:user`) — token value must NOT be visible

<img width="1910" height="651" alt="image" src="https://github.com/user-attachments/assets/5692602a-1452-4d36-b93c-12ef78b96671" />


---

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create and configure the `.mcp.json` file to define the GitHub MCP server.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the full configuration

<img width="1917" height="752" alt="image" src="https://github.com/user-attachments/assets/74d509e1-60db-4f4a-ae7a-0aed700a78ea" />


---

# Task 3 — Add Your Token to settings.local.json

## Goal

Store your GitHub token securely in `.claude/settings.local.json` and ensure it is not committed to version control.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section — **blur or cover the actual GitHub token value**

<img width="1917" height="745" alt="image" src="https://github.com/user-attachments/assets/cc36faa7-0015-482e-a208-96c3f7f47586" />


---

# Task 4 — Verify the Connection with /mcp

## Goal

Confirm that the GitHub MCP server is successfully connected inside Claude Code.

### Evidence

#### Screenshot 4 — `/mcp` output showing `github: connected`

<img width="1917" height="1135" alt="image" src="https://github.com/user-attachments/assets/b9159e1d-a942-41de-957c-35234da860a5" />


---

# Task 5 — Run a Live GitHub Query

## Goal

Verify MCP functionality by retrieving real-time data from your GitHub account using Claude Code.

### Evidence

#### Screenshot 5 — Claude's response showing the GitHub MCP tool call and the retrieved README.md content.

<img width="1917" height="675" alt="image" src="https://github.com/user-attachments/assets/32cda16c-d624-4b97-93d3-e62e3dc428b8" />


---

# Submission Instructions

- Ensure `.mcp.json` is committed to your GitHub repository
- Ensure `.claude/settings.local.json` is NOT committed (must be gitignored)
- Confirm token value is hidden in all screenshots
- Add all required screenshots to your submission
- Push final changes to your forked repository

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/DMIC3-G1-Anishkumar/Ultimate-Agentic-DevOps-with-Claude-Code.git

---

## Security Confirmation

Confirm below:

- [Yes] `settings.local.json` is added to `.gitignore`
- [Yes] GitHub token is NOT exposed in repository or screenshots

---

# Completion Checklist

- [Yes] GitHub PAT created with correct scopes (`repo`, `read:user`)
- [Yes] `.mcp.json` created at project root
- [Yes] `.claude/settings.local.json` contains token (hidden in screenshot)
- [Yes] `.claude/settings.local.json` is NOT committed
- [Yes] `/mcp` shows GitHub connection as active
- [Yes] Live GitHub query returns real repository data
- [Yes] All required screenshots added
- [Yes] GitHub repository URL included

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
