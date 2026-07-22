# Assignment 3 — Building Your Command Center

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a local Claude Skills system by creating the `.claude/skills/` folder structure, adding predefined skill files, and executing a real agentic command (`/scaffold-terraform`) to generate infrastructure code. You will also observe how skills enforce tool restrictions and enable controlled automation.

---

# Task 1 — Create the Skill Folder Structure

## Goal

Create the required `.claude/skills/` directory structure for all skills.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/skills/` folder with all 4 subfolders visible

<img width="1755" height="670" alt="image" src="https://github.com/user-attachments/assets/1bd51aa5-6b7e-45ce-8fbf-b38c9616aa7a" />


---

# Task 2 — Add the Skill Files

## Goal

Place all required skill files into their correct directories and verify their configuration.

### Evidence

#### Screenshot 2 — `.claude/skills/scaffold-terraform/` open in VS Code showing both `SKILL.md` and `template-spec.md`

<img width="1907" height="1136" alt="image" src="https://github.com/user-attachments/assets/43dc1d96-f37e-4e09-96f3-8fcbfaf124ff" />


---

#### Screenshot 3 — Screenshot 3 — `tf-plan/SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no Write) and `disable-model-invocation: true`

<img width="1917" height="1132" alt="image" src="https://github.com/user-attachments/assets/61a265f5-63d8-4efe-9f56-e1a9a71f2982" />


---

# Task 3 — Run /scaffold-terraform

## Goal

Execute the `/scaffold-terraform` skill to generate a full Terraform infrastructure setup.

### Evidence

#### Screenshot 4 — Claude's response showing the scaffold complete with the file list

<img width="1897" height="507" alt="image" src="https://github.com/user-attachments/assets/21559204-a726-45a6-a023-301b46b7f399" />


---

#### Screenshot 5 — VS Code sidebar showing the `terraform/` folder with all generated files inside

<img width="1917" height="1132" alt="image" src="https://github.com/user-attachments/assets/f5d8c99c-5961-474a-a152-14bfbf2426a8" />


---

# Task 4 — Run terraform init and /tf-plan

## Goal

Initialize Terraform and execute the `/tf-plan` skill to observe plan execution and output analysis.

### Evidence

#### Screenshot 6 — Claude's `/tf-plan` response showing it ran the command and analyzed the result (pass or auth error both count)

<img width="1892" height="567" alt="image" src="https://github.com/user-attachments/assets/d8bd2932-aedb-4c01-ae3d-58828ad0c7db" />


---

# Submission Instructions

- Ensure `.claude/skills/` folder and all skill files are committed to your GitHub repository
- Run all commands successfully and capture required screenshots
- Push final changes to your forked repository

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/DMIC3-G1-Anishkumar/Ultimate-Agentic-DevOps-with-Claude-Code.git

## LinkedIn post URL

Paste your forked repository URL here:

`Add your URL here`
---

# Completion Checklist

- [Yes] `.claude/skills/` folder created with all 4 skill folders
- [Yes] All skill files placed correctly
- [Yes] `tf-plan/SKILL.md` shows correct `allowed-tools` restrictions
- [Yes] `/scaffold-terraform` executed successfully
- [Yes] Terraform files generated inside `terraform/` folder
- [Yes] `terraform init` executed successfully
- [Yes] `/tf-plan` executed and output analyzed by Claude
- [Yes] All required screenshots added
- [Yes] GitHub repository URL included
- [ ] LinkedIn post URL included

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
