# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

<img width="1748" height="530" alt="image" src="https://github.com/user-attachments/assets/a68b9181-b672-4eb9-ad9e-ed460830f882" />


### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

The MCP server needs the Jira site URL to know which Atlassian instance it should connect to, and it needs my account email together with the API token to authenticate as my Jira user. The token proves authorization, while the URL and email identify the correct Jira site and account.

---

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

<img width="1438" height="390" alt="image" src="https://github.com/user-attachments/assets/21ac73d0-d4aa-4bae-a075-f0f3fd41d9e0" />


### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

The Jira and GitHub MCP blocks use the same overall MCP structure: a server name, a command, arguments, and environment/configuration inputs. The difference is only how the server process starts — GitHub used npx for a Node.js package while Jira uses uvx for a Python package. Claude Code does not care which programming language the MCP server is written in because both communicate through the same Model Context Protocol interface.

---

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

<img width="1482" height="460" alt="image" src="https://github.com/user-attachments/assets/0c720b67-fce3-4b7e-932a-e1b819b1c081" />


### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

JIRA_API_TOKEN must stay in settings.local.json because it is a secret credential specific to my machine and account. .mcp.json is project configuration that may be committed and shared, so putting the token there could expose it in Git history. Keeping the token in a gitignored local settings file separates reusable configuration from sensitive credentials.

---

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

<img width="1477" height="798" alt="image" src="https://github.com/user-attachments/assets/3d6cac40-cfe6-4850-b3e7-05afaf84cc5b" />

---

# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

<img width="1103" height="636" alt="image" src="https://github.com/user-attachments/assets/407bc2de-5b83-4716-980b-eac5fbfb0167" />


### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

Two independent, verifiable sources were used — not something Claude generated from memory:

1. Jira MCP calls (jira_get_agile_boards, jira_get_sprints_from_board, jira_get_sprint_issues) hit my real Atlassian Cloud instance (anishkumar1404.atlassian.net) over the API. The responses included things a guess couldn't produce: real issue IDs (10035–10037), real browse_url links, exact timestamps, and your actual account ID/email as assignee/reporter.
2. The browser screenshot came from actually navigating Chrome to https://anishkumar1404.atlassian.net/jira/software/projects/DMIWAK/boards/34 and capturing a live screenshot of the rendered page — that's pixel data from my real logged-in session, not text Claude composed.


---

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

<img width="1545" height="973" alt="image" src="https://github.com/user-attachments/assets/c3bdd7a0-1f5e-46e6-9b0f-b85d40cf67ba" />


#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

<img width="767" height="732" alt="image" src="https://github.com/user-attachments/assets/8447cfe8-6d33-413f-b48b-b95335ef9e3d" />



### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

The skill includes only Jira MCP tools that read sprint and issue information, such as sprint/issue search and issue-detail retrieval, plus Read. It deliberately excludes issue creation, issue updates, transitions, comments, assignment changes, and deletion tools.

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

A Scrum Master especially benefits from this restriction because the role should inspect progress, identify blockers, facilitate decisions, and maintain transparency without silently changing the team’s work. If an AI acting as Scrum Master could transition or edit tickets automatically, the board could stop reflecting the team’s actual decisions and become less trustworthy.

---

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

<img width="771" height="652" alt="image" src="https://github.com/user-attachments/assets/93a3a76e-fa78-4630-a796-a54157ccceb4" />


### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

Gather: The Jira MCP tools read the current Sprint, issue statuses, estimates, and related details from the live board.
Analyze: /sprint-health evaluates the retrieved data to calculate progress and identify at-risk or unestimated items.
Human Act: I manually changed the Jira ticket in the browser. This step must remain human because changing status, estimates, or other ticket data affects the shared source of truth and represents an explicit team decision.
Verify: I ran /sprint-health again and confirmed the updated report reflected the manual Jira change without the skill modifying anything itself.

---

# Submission Instructions

Complete all tasks in sequence.

Your submission must include:
- All 8 required screenshots
- All the required notes

---

# Completion Checklist

- [ ] Task 1: Jira API token created, value never screenshotted (Screenshot 1)
- [ ] Task 2: `.mcp.json` has the Jira server block (Screenshot 2)
- [ ] Task 3: Credentials stored in `settings.local.json`, token blurred, file gitignored (Screenshot 3)
- [ ] Task 4: `/mcp` shows the Jira server connected (Screenshot 4)
- [ ] Task 5: Live query returned real sprint data, verified against the browser (Screenshot 5)
- [ ] Task 6: `/sprint-health` skill created with correct read-only `allowed-tools`, and produced a full report (Screenshots 6–7)
- [ ] Task 7: A manual board change was reflected in a second `/sprint-health` run (Screenshot 8)
- [ ] Skill never created, edited, transitioned, or commented on any issue
- [ ] Reflection answered (Notes)
- [ ] No API token value exposed

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
