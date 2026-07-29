# Assignment 2 — CodeTrack: Tracking, Staging, Committing + Deploy to EC2

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will track and stage project files, create two meaningful Git commits in `CodeTrack`, verify your commit history, and deploy the CodeTrack static website to an EC2 instance using Nginx. This connects local version-control practice with a basic manual deployment workflow used in real DevOps environments.

---

# Task 1 — Verify Git Setup and Enter the Repository

## Goal

Confirm that Git works and that you are inside the correct `CodeTrack` repository.

### Evidence

#### Screenshot 1 — Output of `pwd` showing you're inside `CodeTrack`

<img width="696" height="102" alt="image" src="https://github.com/user-attachments/assets/1154419c-008e-47b4-870c-8214afea8e2a" />



---

#### Screenshot 2 — Output of `git status` showing no "not a git repository" error

<img width="837" height="175" alt="image" src="https://github.com/user-attachments/assets/fdcaebd5-ae59-4104-9fb4-4a0183d87efc" />



---

# Task 2 — Create index.html and style.css

## Goal

Create the two starter UI files inside `CodeTrack`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `index.html` and `style.css`

<img width="592" height="307" alt="image" src="https://github.com/user-attachments/assets/443d589b-6038-4955-b7c1-79164fce01a4" />



---

# Task 3 — Add Starter Content

## Goal

Copy the provided starter HTML and CSS content into your local `index.html` and `style.css` files.

### Evidence

#### Screenshot 4 — Your editor showing the contents of `index.html` and `style.css`

<img width="1506" height="1062" alt="image" src="https://github.com/user-attachments/assets/4f2e382a-1cd1-4468-866a-ccb10e24c3cf" />


---

# Task 4 — Track and Stage Files Correctly

## Goal

Confirm both files show as untracked, then stage them individually with `git add`.

### Evidence

#### Screenshot 5 — Output of `git status` showing both files as untracked

<img width="882" height="550" alt="image" src="https://github.com/user-attachments/assets/c3198bfe-9be8-4b38-abb0-c349cf8ae8f1" />


---

#### Screenshot 6 — Output of `git status` showing both files staged under "Changes to be committed"

<img width="682" height="380" alt="image" src="https://github.com/user-attachments/assets/ae2e9d0a-81aa-48fc-aa16-ae4354ed3eea" />


---

# Task 5 — Create the First Commit (Clean Initial Commit)

## Goal

Commit the staged starter files using the message `Initial UI scaffold: add index.html and style.css`, then check the log.

### Evidence

#### Screenshot 7 — Output of `git commit`

<img width="822" height="161" alt="image" src="https://github.com/user-attachments/assets/9a3a8d15-a417-437f-89c0-09773fddeffe" />


---

#### Screenshot 8 — Output of `git log --oneline` showing the first commit

<img width="802" height="172" alt="image" src="https://github.com/user-attachments/assets/57d35de6-5ed0-4b64-9a68-10bf4c64f742" />


---

# Task 6 — Modify index.html and Create a Second Commit

## Goal

Follow the instruction comment inside `index.html` to update the Student Name and Group Name, then commit that change separately using the message `Update homepage content: heading, tagline, CTA button`.

### Evidence

#### Screenshot 9 — Browser showing the updated page with your Student Name and Group Name visible

<img width="1075" height="521" alt="image" src="https://github.com/user-attachments/assets/578bbbea-5353-45d4-9966-2c3526465059" />


---

#### Screenshot 10 — Output of `git status` showing `index.html` as modified

<img width="977" height="222" alt="image" src="https://github.com/user-attachments/assets/220e6bd8-b3eb-42a8-862c-13c7f3c15e9f" />


---

#### Screenshot 11 — Output of `git commit`

<img width="900" height="287" alt="image" src="https://github.com/user-attachments/assets/3fd602f7-0832-4929-a420-6bf38e27ad72" />


---

#### Screenshot 12 — Output of `git log --oneline` showing two commits

<img width="860" height="300" alt="image" src="https://github.com/user-attachments/assets/6cc55ad8-bcff-427d-8dad-1af7e1c24319" />



---

# Task 7 — Deploy to EC2 with Nginx (Static Website)

## Goal

Install and start Nginx on your EC2 instance, then copy `index.html` and `style.css` into the Nginx web root.

### Evidence

#### Screenshot 13 — Output of `systemctl status nginx --no-pager` showing Nginx `active (running)`

<img width="967" height="577" alt="image" src="https://github.com/user-attachments/assets/c3ddce36-6926-406a-9a58-2932fafc0349" />


---

#### Screenshot 14 — Output of `curl -I http://localhost` showing `HTTP/1.1 200 OK`

<img width="875" height="232" alt="image" src="https://github.com/user-attachments/assets/6b529b48-b819-4542-98cb-7c43d6915568" />


---

#### Screenshot 15 — Browser showing the CodeTrack site loaded at `http://<EC2_PUBLIC_IP>`, with your Full Name and Group Name visible

<img width="1917" height="1087" alt="image" src="https://github.com/user-attachments/assets/55ca56cd-1301-4e93-a8b6-e4f400ac7b67" />


---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — LinkedIn post showing the deployed CodeTrack application

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name and Group Name must be visible in the deployed application evidence
- `git log --oneline` output must show at least two meaningful commits
- Do not expose AWS access keys, passwords, private key contents, or other sensitive information

---

# Completion Checklist

- [ ] `CodeTrack` repository verified with `git status` (Screenshots 1–2)
- [ ] `index.html` and `style.css` created and populated (Screenshots 3–4)
- [ ] Starter files staged and committed in the first commit (Screenshots 5–8)
- [ ] Student Name and Group Name updated in `index.html` (Screenshot 9)
- [ ] Second controlled commit created (Screenshots 10–12)
- [ ] Nginx active on the EC2 instance and CodeTrack reachable via its public IP (Screenshots 13–15)
- [ ] LinkedIn post published and URL submitted
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
