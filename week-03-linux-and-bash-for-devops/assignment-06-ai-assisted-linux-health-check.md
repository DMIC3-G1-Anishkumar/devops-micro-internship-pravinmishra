# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

<img width="942" height="341" alt="image" src="https://github.com/user-attachments/assets/d4236511-1df5-4f3a-ad1c-30dac5a6f1b7" />


---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

<img width="1907" height="386" alt="image" src="https://github.com/user-attachments/assets/b8690dc9-b0ef-44c7-8359-2fefceb2f9c7" />


---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

systemctl is-active nginx returning active proves the Nginx service is running.

---

**2. What proves that the server is listening for HTTP traffic?**

ss -ltn | grep ':80' proves that a process is listening for HTTP traffic on port 80.

---

**3. Why must you capture a healthy baseline before simulating an incident?**

A healthy baseline provides normal evidence that can be compared with the failed and recovered states.

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

<img width="1917" height="896" alt="image" src="https://github.com/user-attachments/assets/dc86c33c-9cc1-4dc4-a923-521097559f4e" />


---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Project-specific rules help Claude understand the intended workflow, output format and operational restrictions.

---

**2. Why is the human required to execute the recovery command?**

The human must execute recovery commands because restarting or changing a service can affect availability and production workloads.

---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The rule stating that Claude must not claim a root cause without supporting evidence prevents unsupported diagnosis.

---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

<img width="1917" height="891" alt="image" src="https://github.com/user-attachments/assets/9013552b-2112-4c92-bc9a-fde9010d2150" />



---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

Claude's read-only inspection commands represent the Gather phase.

---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

I verified that Claude did not create files by checking status and listing the project files.

---

**3. Why is planning before coding useful in DevOps automation?**

Planning helps identify required checks, thresholds, safety limits and expected outputs before implementation.

---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

<img width="1917" height="771" alt="image" src="https://github.com/user-attachments/assets/ce8b8641-938b-4303-a306-fffe9668aadd" />


---

#### Screenshot 6 — Middle section showing check functions and conditionals

<img width="1917" height="796" alt="image" src="https://github.com/user-attachments/assets/aaabea99-b0df-4729-bea7-efe3f1f0f835" />


---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

<img width="1917" height="820" alt="image" src="https://github.com/user-attachments/assets/228f809b-a63c-40fb-bb78-ed13bc052ff2" />


---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

<img width="1910" height="902" alt="image" src="https://github.com/user-attachments/assets/d21a59a1-adfe-4504-8c1b-e7ec4c9de2df" />


---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the five health checks.

---

**2. How does the `for` loop use that array?**

The 'for' loop reads each array item and executes the matching function.

---

**3. Why are the health checks separated into functions?**

Functions keep each check separate, reusable and easier to test.

---

**4. What is the purpose of `$(...)` in this script?**

$(...) runs a command and stores its output in a variable.

---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes allow other tools to distinguish healthy, warning and failed results.

---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

<img width="1907" height="896" alt="image" src="https://github.com/user-attachments/assets/f750f256-7f80-4eef-b381-7a0457d0829c" />


---

#### Screenshot 10 — Output showing the captured exit code and final summary

<img width="1877" height="692" alt="image" src="https://github.com/user-attachments/assets/345fbe50-9553-422c-9e36-e5fd0ede9f31" />


---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The expected healthy baseline status is HEALTHY.

---

**2. Which exact Linux evidence proves the application is serving traffic?**

Port 80 listening and an HTTP 200 response from curl prove that the application is serving traffic.

---

**3. Did your script return exit code 0 or 1? Explain why.**

The script should return exit code 0 because all five checks passed.

---

**4. What is the difference between a warning and a failure in this script?**

A warning indicates a degraded condition that still works; a failure indicates that a critical check did not pass.

---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

<img width="1917" height="905" alt="image" src="https://github.com/user-attachments/assets/27598c76-4ebb-4675-b546-99e020287e2d" />

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

<img width="1917" height="915" alt="image" src="https://github.com/user-attachments/assets/416b54cb-ae16-4f4c-9b95-bf3bf3c16a33" />


---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

Bash gathers evidence, while Read and Grep inspect reports. Write is excluded because the workflow must remain read-only.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

disable-model-invocation: true helps ensure that the skill runs only when the human explicitly invokes it.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash gathers system evidence; Claude interprets and explains that evidence.

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

The skill bases its conclusion on repeatable Linux evidence instead of guessing from a general question.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

<img width="1902" height="285" alt="image" src="https://github.com/user-attachments/assets/61ff8eec-034c-4879-bb0f-c95a333c70a5" />


---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

<img width="1917" height="906" alt="image" src="https://github.com/user-attachments/assets/d23dec04-e398-455a-962b-eccddfa0c5fb" />



---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

<img width="1907" height="906" alt="image" src="https://github.com/user-attachments/assets/b3899b84-1cd5-4cf1-acec-716d7ed64565" />


---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

Nginx Service
HTTP Port 80
Local HTTP Response

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

systemctl reported the Nginx service as inactive, there was no process listening on port 80, and the HTTP request to http://localhost failed.

---

**3. Did Claude execute the recovery command? Why is that important?**

No. Claude only suggested the recovery command. This is important because recovery actions should be approved and executed by a human to avoid unintended changes.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**
The Bash report represents the Gather phase because it collects system health evidence.

---

**5. Which phase is represented by Claude's explanation?**

Claude's explanation represents the Analyze phase because it interprets the collected evidence and identifies the most likely cause.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

<img width="1042" height="441" alt="image" src="https://github.com/user-attachments/assets/415358c2-a4b7-4753-bbf3-5391727054a1" />


---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

<img width="1912" height="911" alt="image" src="https://github.com/user-attachments/assets/31b372f0-2034-4cf2-b801-25dd50c09949" />


---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

<img width="947" height="150" alt="image" src="https://github.com/user-attachments/assets/bc19b038-70df-402c-8232-9ed678cbf914" />


---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

<img width="1917" height="900" alt="image" src="https://github.com/user-attachments/assets/514e2d88-d83a-46a4-9a5b-d8a96d4d0c59" />


---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

I manually restarted the Nginx service using sudo systemctl start nginx.

---

**2. What evidence proves that the service recovered?**

The Nginx service became active, port 80 was listening, curl -I http://localhost returned HTTP/1.1 200 OK, and the recovery triage report showed no failed checks.

---

**3. Why is the second triage run necessary?**

The second triage run confirms that the recovery action successfully restored the service and verifies that no health issues remain.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

It could hide the real cause of the failure, interrupt running applications, create restart loops, or make an existing problem worse without human approval.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

A chatbot provides general answers, while an agentic AI workflow collects real system evidence, analyzes it, waits for human approval, and verifies the outcome.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Anish Kumar

**Date:** 28/07/2026

---

**1. Reported Symptom**

The React application became unavailable because the Nginx service was stopped. HTTP requests to the local server failed, making the website inaccessible.

---

**2. Evidence Collected**

The Bash triage script showed that the Nginx service was inactive, there was no process listening on port 80, and the HTTP request to `http://localhost` failed. Disk and memory usage remained within healthy limits.

---

**3. Most Likely Cause**

The Nginx service had been stopped, preventing it from listening on port 80 and serving the React application.

---

**4. Human-Approved Recovery Action**

After reviewing the evidence and Claude's recommendation, I manually executed:

```bash
sudo systemctl start nginx
```

to restore the Nginx service.

---

**5. Verification**

After restarting Nginx, `systemctl is-active nginx` returned **active**, port 80 was listening, `curl -I http://localhost` returned **HTTP/1.1 200 OK**, and the second Linux triage report showed no failed checks.

---

**6. Safety Decision**

The AI assistant did not perform any recovery actions automatically. It remained read-only, collected evidence, analyzed the incident, and suggested a recovery command, while the final recovery action was performed manually by the human operator.

---

**7. Agentic Loop Mapping**

- **Gather:** The Bash triage script collected Linux and Nginx health information.
- **Analyze:** Claude analyzed the collected evidence and identified the most likely cause.
- **Human Act:** I manually restarted the Nginx service.
- **Verify:** The triage script was executed again to confirm that the service recovered successfully and all checks passed.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`Add your URL here`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
- [ ] No sensitive data exposed

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
