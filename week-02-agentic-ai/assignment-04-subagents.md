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

<img width="1912" height="1132" alt="image" src="https://github.com/user-attachments/assets/a378e5cc-2b29-4002-8658-51d631146dfc" />


---

# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?
Answer:
The cost optimizer performs lightweight analysis tasks such as checking Terraform resources and identifying possible cost-saving improvements. Since it does not require deep reasoning like security analysis, the faster and more cost-efficient Haiku model is suitable for this task.

---

#### 2. Why does the security auditor NOT have Write in its tools list?

Answer:
The security auditor is designed only to inspect and analyze Terraform configurations. Removing Write permission prevents accidental modification of infrastructure files and follows the principle of least privilege.
---

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

Answer:
The Terraform writer needs flexibility because it performs code generation and modification tasks. Using inherit allows it to use the default model configuration from Claude Code instead of forcing a fixed model.

---

### Evidence

#### Screenshot 2 — `security-auditor.md` frontmatter showing model and tools configuration

<img width="1917" height="977" alt="image" src="https://github.com/user-attachments/assets/0546565a-f0a7-42b1-9ce1-e3e7951242b1" />


---

#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

<img width="1917" height="1140" alt="image" src="https://github.com/user-attachments/assets/f202ee54-3d04-49c5-bb16-723428f3c4f8" />


---

# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — The delegation message showing Claude launched the security-auditor

<img width="1917" height="1142" alt="image" src="https://github.com/user-attachments/assets/177ec84a-f621-4c22-b482-dc5f9563fd97" />


---

#### Screenshot 5 — Security audit report output

<img width="1917" height="1130" alt="image" src="https://github.com/user-attachments/assets/50db046b-48d6-4ded-8ebd-4bc276a0ee94" />


---

# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — The full cost optimization report

<img width="1917" height="1135" alt="image" src="https://github.com/user-attachments/assets/c5385359-7145-40cb-8346-f6ef34ca7bb9" />


---

# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your GitHub Repo
- Push final changes to your forked GitHub repository

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/DMIC3-G1-Anishkumar/Ultimate-Agentic-DevOps-with-Claude-Code.git

---

# Completion Checklist

- [Yes] `.claude/agents/` folder contains all 3 agent files
- [Yes] Screenshot 2 shows correct `security-auditor.md` configuration
- [Yes] Screenshot 3 shows correct `cost-optimizer.md` configuration
- [Yes] All 3 written answers completed 
- [Yes] Security auditor executed successfully
- [Yes] Cost optimizer executed successfully
- [Yes] Security report is visible with findings
- [Yes] Cost report is visible with recommendations
- [Yes] All required screenshots added
- [Yes] GitHub repo updated with agents

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
