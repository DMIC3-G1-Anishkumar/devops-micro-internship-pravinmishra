# Assignment 3 — CodeTrack: Branching Workflow (Add & Verify a Contact Page)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will add a new Contact page to CodeTrack using a clean feature-branch workflow. You will keep each change in a separate commit, prove that your default branch remains unchanged before the merge, and validate the result after merging.

---

# Task 1 — Confirm Repository State and Default Branch

## Goal

Start from a clean default branch (`main` or `master`) and confirm the repository status.

### Evidence

#### Screenshot 1 — Output of `git status` and `git branch` showing a clean status and the default branch checked out

<img width="671" height="282" alt="image" src="https://github.com/user-attachments/assets/c4514c33-b79d-4a08-bd1d-abe4800fec8c" />


---

# Task 2 — Create and Switch to a Feature Branch

## Goal

Create a branch named exactly `feature/contact-page` and switch to it.

### Evidence

#### Screenshot 2 — Output of `git checkout -b feature/contact-page` and `git branch` showing `* feature/contact-page`

<img width="782" height="302" alt="image" src="https://github.com/user-attachments/assets/712c0355-4598-4b7d-8046-e067fea6cc54" />


---

# Task 3 — Add contact.html on the Feature Branch

## Goal

Create `contact.html` with the provided content and commit it alone using the message `feat(contact): add Contact page`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `contact.html`

<img width="891" height="107" alt="image" src="https://github.com/user-attachments/assets/cdc767b8-694f-44f5-99e8-5d44894e869a" />

---

#### Screenshot 4 — Output of `git commit`

<img width="936" height="192" alt="image" src="https://github.com/user-attachments/assets/0e945e50-5931-47e2-84bf-33ebba8abaf6" />


---

#### Screenshot 5 — Output of `git log --oneline -3` showing the new commit

<img width="795" height="137" alt="image" src="https://github.com/user-attachments/assets/bc6d0667-91f0-403c-8014-0134a62bf4c4" />


---

# Task 4 — Add the Contact Link to index.html

## Goal

Add the provided Contact Page link to `index.html` and commit it separately using the message `feat(nav): add Contact Page link`.

### Evidence

#### Screenshot 6 — Output of `git status` showing `index.html` as modified before staging

<img width="747" height="326" alt="image" src="https://github.com/user-attachments/assets/f0f07bb8-b170-48f2-8913-b8d5be348566" />


---

#### Screenshot 7 — Output of `git commit`

<img width="1041" height="172" alt="image" src="https://github.com/user-attachments/assets/62abfc6f-3fec-41e5-8bc4-fe82f0718015" />


---

#### Screenshot 8 — Browser showing the Contact Page link on the homepage while on `feature/contact-page`

<img width="1905" height="1025" alt="image" src="https://github.com/user-attachments/assets/a6bac251-99fd-4681-afb4-b5b89ae97953" />



---

# Task 5 — Verify Isolation (Prove the Default Branch Is Unchanged)

## Goal

Switch back to the default branch and confirm that `contact.html` and the Contact Page link do not exist there yet.

### Evidence

#### Screenshot 9 — Terminal showing the checkout and `ls` output, proving `contact.html` is absent

<img width="715" height="352" alt="image" src="https://github.com/user-attachments/assets/5b7f5ca9-11ed-4991-85c4-2ea40d6ccea2" />



---

#### Screenshot 10 — Browser showing the homepage on the default branch with no Contact Page link

<img width="1887" height="952" alt="image" src="https://github.com/user-attachments/assets/fe414ec9-58eb-4641-8f49-58f2f8da7e70" />


---

# Task 6 — Merge the Feature Branch into the Default Branch

## Goal

Merge `feature/contact-page` into your default branch and confirm the Contact page works.

### Evidence

#### Screenshot 11 — Output of `git merge feature/contact-page`

<img width="792" height="197" alt="image" src="https://github.com/user-attachments/assets/751ebe41-715e-4d03-b9ee-bebe9c0a87b9" />


---

#### Screenshot 12 — Output of `ls` showing `contact.html` after the merge

<img width="651" height="180" alt="image" src="https://github.com/user-attachments/assets/52fd6040-d944-4be6-a9ce-1f154c4c3bdc" />


---

#### Screenshot 13 — Browser showing the Contact page opened from the homepage link on the default branch

<img width="1367" height="396" alt="image" src="https://github.com/user-attachments/assets/018fe025-8920-41db-99be-97daec89b9a7" />

---

# Task 7 — Inspect History (Graph View)

## Goal

Display the repository history as a graph and locate both feature commits.

### Evidence

#### Screenshot 14 — Full output of `git log --oneline --graph --decorate --all`

<img width="872" height="152" alt="image" src="https://github.com/user-attachments/assets/a426da2a-0381-4d35-bb83-6524283d36f3" />


---

# Task 8 — Optional Cleanup (Delete the Feature Branch)

## Goal

Delete the merged `feature/contact-page` branch to keep your branch list clean.

### Evidence

#### Screenshot 15 (Optional) — Output showing `feature/contact-page` deleted and no longer listed

<img width="621" height="182" alt="image" src="https://github.com/user-attachments/assets/34e93b2b-7716-42de-b9aa-3e326fc576b7" />


---

# Submission Instructions

- Tasks 1–7 are required; Task 8 is optional
- Add all required screenshots in your submission
- Evidence must show `contact.html` and the homepage link were absent before merging, and working after merging
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [ ] Repository confirmed clean on the default branch (Screenshot 1)
- [ ] `feature/contact-page` created and checked out (Screenshot 2)
- [ ] `contact.html` added in its own commit (Screenshots 3–5)
- [ ] Homepage Contact link added in a separate commit (Screenshots 6–8)
- [ ] Default branch proven unchanged before merge (Screenshots 9–10)
- [ ] Feature branch merged and Contact page verified (Screenshots 11–13)
- [ ] Graph history reviewed (Screenshot 14)
- [ ] Optional cleanup completed (Screenshot 15)
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
