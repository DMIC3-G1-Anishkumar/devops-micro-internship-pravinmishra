# Assignment 4 — Gotto Job: Backlog Refinement & Sprint 1 in Jira

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this 90-minute, time-boxed exercise, you will act as a Scrum team — or run in Solo Mode, playing every role yourself — to turn the Gotto Job template into a value-ordered backlog, estimate the work in story points, plan Sprint 1, open the burndown chart, and ship one small UI-only increment (text, color, spacing, a label, or a CTA — no backend changes).

---

# Task 1 — Roles & Mode Setup (Team vs Solo)

## Goal

Choose Team Mode or Solo Mode, and document how each Scrum role (Product Owner, Scrum Master, Dev Lead, DevOps Lead) was handled.

### Evidence

#### Screenshot 1 — Jira "Create project" screen, or the project sidebar after creation

<img width="1906" height="1027" alt="image" src="https://github.com/user-attachments/assets/e79d3b24-9428-41b0-8a43-d5f6b6329bd9" />


---

### Notes

Write one line for each role: PO (what you prioritized), SM (how you ensured process), Dev Lead (what you built), DevOps Lead (how you shipped).

* **PO (Product Owner):** I prioritized the backlog based on user value and selected the most practical Story to deliver within the available time.

* **SM (Scrum Master):** I followed the Scrum process by keeping the work timeboxed, updating the board, and completing the required Sprint activities and retrospective.

* **Dev Lead:** I implemented the selected UI change by updating the Gotto Job website and verifying that the change worked as expected.

* **DevOps Lead:** I committed the change in Git, deployed it to EC2 through Nginx, and verified that the updated website was live on the public URL.


---

# Task 2 — Create the Jira Project (Team-managed → Scrum)

## Goal

Create a Team-managed Scrum project named `Gotto Job – Team <#>` (Team Mode) or `Gotto Job – <YourName>` (Solo Mode).

### Evidence

#### Screenshot 2 — Project created page showing the project name and key

<img width="1906" height="1027" alt="image" src="https://github.com/user-attachments/assets/f9de0bae-07f7-4067-a965-a57a2d264fbf" />


---

# Task 3 — Create the Epic

## Goal

Create the Epic `Improve Gotto Job UI discoverability & trust` to group the UI improvement initiative.

### Evidence

#### Screenshot 3 — Backlog showing the Epic panel with the Epic visible

<img width="1486" height="965" alt="image" src="https://github.com/user-attachments/assets/00b78e99-03a1-4e50-916c-8c2783f858f1" />



---

# Task 4 — Seed the Product Backlog (6–8 Stories + Fibonacci Points + Ranking)

## Goal

Create at least six Stories under the Epic, estimate each with 1, 2, or 3 story points, and rank them by value.

### Evidence

#### Screenshot 4 — Backlog showing the Epic and at least six Stories under it

<img width="1482" height="960" alt="image" src="https://github.com/user-attachments/assets/988c0a32-59ca-429d-8ecd-a87759ba496f" />


---

#### Screenshot 5 — One Story opened showing its Story Points and acceptance criteria filled in

<img width="1501" height="947" alt="image" src="https://github.com/user-attachments/assets/1a83b60a-bc32-4131-983d-9af1bafa9831" />


---

# Task 5 — Planning Poker (Estimate + Debate Notes)

## Goal

Confirm the Story Points (1, 2, or 3) for each Story and record brief reasoning for each estimate.

### Evidence

#### Screenshot 6 — Backlog showing Story Points visible, or two or three Stories opened showing their points

<img width="1597" height="990" alt="image" src="https://github.com/user-attachments/assets/89f4d92b-315a-44a4-b228-b71083dfc17f" />
<img width="1558" height="982" alt="image" src="https://github.com/user-attachments/assets/b43db067-486c-44cb-8360-a0e789bf7b65" />
<img width="1582" height="997" alt="image" src="https://github.com/user-attachments/assets/57ab9376-5bef-4337-b94c-9b30e9f570ed" />




---

### Notes

For each story, explain in one or two lines why it is a 1, 2, or 3 (mention any debate, even in Solo Mode).

S1 – Hero tagline (1 point): This is a very small change because only one heading needs to be updated. It does not require any additional logic or major testing.
S2 – Button colour (1 point): This mainly requires changing the button colour in CSS. Even though multiple buttons may be affected, the change itself is simple and easy to verify.
S3 – Job card typography (2 points): This needs changes to the font size and weight, followed by checks to make sure the job cards still look good on different screen sizes.
S4 – REMOTE badge (2 points): This is slightly more complex because a new badge needs to be added and shown only for remote jobs, so some additional logic and testing are required.
S5 – Posted on date (1 point): This is a simple text addition and does not involve any complex functionality, so it is a small task.
S6 – Search labels (2 points): Multiple labels and placeholders need to be updated and verified, so it requires more effort than changing a single text element.
S7 – Job Detail "Apply Now" Button (1 point): This only requires adding one button with a link to an email address or placeholder URL. Since there is no extra logic involved, it is a simple change.
S8 – Footer Trust Links (1 point): This requires adding only two footer links, "About" and "Contact". It is a small HTML update with no complex functionality.

---

# Task 6 — Sprint Planning: Create Sprint 1 + Sprint Goal + Scope

## Goal

Create Sprint 1, move three or four Stories into it (approximately 3–6 points), set the Sprint Goal, and break each selected Story into Build, Verify, Deploy, and Screenshot Sub-tasks.

### Evidence

#### Screenshot 7 — Sprint 1 with the selected Stories inside it

<img width="1292" height="298" alt="image" src="https://github.com/user-attachments/assets/fca1cfbf-20f3-4533-9291-57cd24d8862f" />



---

#### Screenshot 8 — One Story showing the Sub-tasks created

<img width="1593" height="987" alt="image" src="https://github.com/user-attachments/assets/9b43dd8f-71ab-4a8a-8066-6d92aa8c93e9" />


---

# Task 7 — Reports: Open Burndown Chart

## Goal

Open the Burndown Chart and confirm it exists for Sprint 1. It is acceptable if the chart is not yet populated.

### Evidence

#### Screenshot 9 — Burndown Chart page opened, even if empty

<img width="1563" height="966" alt="image" src="https://github.com/user-attachments/assets/b0f486fa-7204-4cc8-8bec-9505133ea522" />

---

# Task 8 — Ship One Small Increment (Build + Deploy + Proof)

## Goal

Implement one small UI-only Story from Sprint 1, commit it, deploy it live, and move the Story and its Sub-tasks to Done in Jira.

### Evidence

#### Screenshot 10 — Jira board showing the Story moved to Done

<img width="1587" height="983" alt="image" src="https://github.com/user-attachments/assets/8911f194-ac0c-4efe-b0dd-1fadd2599f65" />


---

#### Screenshot 11 — Git commit output

<img width="1208" height="1047" alt="image" src="https://github.com/user-attachments/assets/f0f3db97-6e51-4a85-8b42-9ff4c1a3cd52" />


---

#### Screenshot 12 — Live URL in the browser showing the UI change, with the URL visible

<img width="1907" height="1087" alt="image" src="https://github.com/user-attachments/assets/cba7bb91-9124-4422-b2f7-380e77107f1b" />


---

# Task 9 — Retro Notes (Scrum Pillar + Value)

## Goal

Add a retro comment covering what went well, what to improve, one Scrum pillar observed (Transparency, Inspection, or Adaptation), and one Scrum value (Openness, Focus, Commitment, Courage, or Respect).

### Evidence

#### Screenshot 13 — Jira retro comment visible

<img width="1902" height="1027" alt="image" src="https://github.com/user-attachments/assets/afc06107-1641-4cdc-befd-17ba7384f389" />


---

# Task 10 — LinkedIn Post (Mandatory)

## Goal

Publish a LinkedIn post about what you delivered, including your live URL, three to five lines on what you did and learned, and one screenshot (Burndown Chart, Sprint board, or the live UI change).

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot 14 — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all 14 required screenshots
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Team Mode or Solo Mode selected and all four roles documented (Screenshot 1 & Notes)
- [ ] Task 2: Team-managed Scrum project created with the required name (Screenshot 2)
- [ ] Task 3: UI improvement Epic created (Screenshot 3)
- [ ] Task 4: 6–8 Stories added under the Epic and ranked by value (Screenshots 4 & 5)
- [ ] Task 5: Story Points set (1, 2, or 3) with reasoning recorded (Screenshot 6 & Notes)
- [ ] Task 6: Sprint 1 created with Sprint Goal, 3–4 Stories, and Sub-tasks (Screenshots 7 & 8)
- [ ] Task 7: Burndown Chart opened (Screenshot 9)
- [ ] Task 8: One UI-only increment implemented, committed, deployed, and verified (Screenshots 10–12)
- [ ] Task 9: Retro comment with one Scrum pillar and one Scrum value (Screenshot 13)
- [ ] Task 10: Mandatory LinkedIn post published with the live URL, backlog refinement, Sprint planning, one shipped increment, proof, and Screenshot 14
- [ ] Full Name visible in required screenshots
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
