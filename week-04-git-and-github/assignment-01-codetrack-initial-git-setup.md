# Assignment 1 — CodeTrack: Initial Git Setup (Local Only)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will set up Git correctly on your local machine before starting the CodeTrack project. You will create a local repository and configure your Git identity at both the repository level (local) and the machine level (global). This assignment is local only — you will not push anything to GitHub yet.

---

# Task 1 — Create the CodeTrack Project and Initialize Git

## Goal

Create a `CodeTrack` project folder and initialize it as a Git repository.

### Evidence

#### Screenshot 1 — Output of `git init` inside `CodeTrack` showing "Initialized empty Git repository"

<img width="827" height="286" alt="image" src="https://github.com/user-attachments/assets/cb19c5ef-8a02-471c-a668-797e5e43734a" />



---

#### Screenshot 2 — Output of `ls -a` showing the `.git` folder

<img width="672" height="201" alt="image" src="https://github.com/user-attachments/assets/c54b76ad-e97b-4c7c-8aee-7a8ce96bf7cf" />



---

### Notes

**1. What is the `.git` folder, and why does it matter?**

The .git folder stores all Git repository information, including commit history, branches, configuration, and tracked-file metadata. It is important because Git uses this folder to recognize the project as a repository and manage its version history. Deleting it removes the repository’s Git history and configuration.

---

# Task 2 — Configure Git Identity Locally (Repository-Only)

## Goal

Set your Git username and email for the `CodeTrack` repository only, using `git config --local`.

### Evidence

#### Screenshot 3 — Output of `git config --local --list` showing your `user.name` and `user.email`

<img width="727" height="470" alt="image" src="https://github.com/user-attachments/assets/73b8c00a-3c7e-48e2-8daa-3e33c6a9b0b3" />



---

# Task 3 — Configure Git Identity Globally

## Goal

Set a global Git username and email for this machine using `git config --global`. Note that CodeTrack's local settings still take priority over these.

### Evidence

#### Screenshot 4 — Output of `git config --global --list` showing your `user.name` and `user.email`

<img width="932" height="127" alt="image" src="https://github.com/user-attachments/assets/85609d20-e4ce-4aa0-9c9b-1c6703804e9b" />



---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [Yes] `CodeTrack` folder created and initialized as a Git repository (Screenshots 1–2)
- [Yes] Explanation of the `.git` folder written in your own words
- [Yes] Local `user.name` and `user.email` configured and verified (Screenshot 3)
- [Yes] Global `user.name` and `user.email` configured and verified (Screenshot 4)
- [Yes] No sensitive data exposed

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
