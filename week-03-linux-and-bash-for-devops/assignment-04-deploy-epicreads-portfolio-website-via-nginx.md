# Assignment 4 — Deploy EpicReads Portfolio Website via Nginx

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will deploy a static portfolio website on an Ubuntu VM using Nginx. You will download the website template, add your ownership proof in the footer, deploy the files to the Nginx web root, and verify the website is publicly accessible via a browser.

---

# Task 0 — Pre-flight Check

## Goal

Verify the Ubuntu VM and Nginx are ready for deployment.

### Evidence

#### Screenshot 0 — Output of `sudo systemctl status nginx --no-pager` showing Active (running)

<img width="1917" height="767" alt="image" src="https://github.com/user-attachments/assets/63de8bdd-26fc-4c8d-9bc8-f65eedc5bfb2" />


---

# Task 1 — Get the Website Source Code

## Goal

Download and extract the portfolio website template.

### Evidence

#### Screenshot 1 — Output of `ls -la` showing the extracted project folder

<img width="1905" height="557" alt="image" src="https://github.com/user-attachments/assets/0b8844dd-5452-4bc3-81e6-5892f147d8bb" />


---

# Task 2 — Add Ownership Proof (Anti-Copy Change)

## Goal

Update the website footer with your deployment details.

### Evidence

#### Screenshot 2 — Nano editor open with the updated footer showing your Full Name, Group, Week, and Date

<img width="1917" height="887" alt="image" src="https://github.com/user-attachments/assets/c1916f56-5b38-4d6f-bef2-540a30b2735f" />


---

# Task 3 — Deploy Website via Nginx

## Goal

Deploy the portfolio website to the Nginx web root.

### Evidence

#### Screenshot 3 — Output of `sudo nginx -t` showing configuration test successful

<img width="1771" height="126" alt="image" src="https://github.com/user-attachments/assets/0581d3a3-6eb8-419c-9db7-c9ac2d0773be" />


---

#### Screenshot 4 — Output of `ls /var/www/html` showing deployed website files

<img width="1315" height="85" alt="image" src="https://github.com/user-attachments/assets/bd45650e-8328-4fe8-ba91-445aa2b0654c" />


---

# Task 4 — Verify Website is Live

## Goal

Verify the deployed website is publicly accessible and the footer contains your details.

### Evidence

#### Screenshot 5 — Output of `curl ifconfig.me` showing the server's public IP address

<img width="1101" height="72" alt="image" src="https://github.com/user-attachments/assets/68286a95-03a8-44eb-b7a2-225d6e8189e5" />


---

#### Screenshot 6 — Browser showing the live website with your Full Name and deployment details in the footer

<img width="1912" height="1081" alt="image" src="https://github.com/user-attachments/assets/d11920a7-cecd-4672-9347-e3058355da40" />


---

# Task 5 — Mini Real DevOps Operational Check

## Goal

Verify the deployed website and Nginx service are healthy.

### Evidence

#### Screenshot 7 — Output of `systemctl is-enabled nginx`

<img width="1906" height="902" alt="image" src="https://github.com/user-attachments/assets/dbd8c445-036f-43c6-a34a-20dc3965865b" />


---

#### Screenshot 8 — Output of `curl -I http://localhost` showing 200 OK

<img width="1911" height="892" alt="image" src="https://github.com/user-attachments/assets/7e2be5c8-68e9-4776-9e60-96ff317b93cf" />


---

# LinkedIn Post (Mandatory)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post showing the live website with your Full Name in the footer

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Ownership proof in the footer is mandatory
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [Yes] Screenshot 0: Nginx service status (active/running)
- [Yes] Screenshot 1: Website files downloaded and extracted
- [Yes] Screenshot 2: Footer updated with Full Name, Group, Week, and Date
- [Yes] Screenshot 3: Nginx configuration test successful
- [Yes] Screenshot 4: Website files deployed to /var/www/html
- [Yes] Screenshot 5: Public IP retrieved
- [Yes] Screenshot 6: Live website accessible in browser with footer details
- [Yes] Screenshot 7: Nginx enabled on boot
- [Yes] Screenshot 8: Local HTTP response returns 200 OK
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
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
