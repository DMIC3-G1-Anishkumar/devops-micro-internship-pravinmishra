# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

<img width="1917" height="867" alt="image" src="https://github.com/user-attachments/assets/78f874ff-1bd3-42a1-9d9d-2a25c637408a" />


---

#### Screenshot 2 — Output of `ip a`

<img width="1506" height="437" alt="image" src="https://github.com/user-attachments/assets/4249a2b8-36d7-46f5-a37e-e2668254f660" />

---

#### Screenshot 3 — Output of `sudo ss -tulpen`

<img width="1897" height="832" alt="image" src="https://github.com/user-attachments/assets/bf09386e-75dc-4dfb-9eb9-a0b2fec6046a" />


---

#### Screenshot 4 — Output of `sudo ufw status`

<img width="1902" height="895" alt="image" src="https://github.com/user-attachments/assets/0fb4f3c6-5f9b-4172-bd18-1fc681371786" />


---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

Nginx is proven to be listening on **0.0.0.0:80** by checking the active listening ports using commands such as: sudo ss -tulpen
If the output shows: LISTEN 0 511 0.0.0.0:80
it confirms that Nginx is bound to **0.0.0.0** on port **80**, meaning it is accepting HTTP connections from any network interface on the server, not just localhost. This verifies that the web server is ready to receive incoming HTTP requests, provided the EC2 Security Group allows traffic on port 80.

---

**2. What proves SSH is active on port 22?**

SSH is proven to be active on **port 22** by checking the listening network ports using: sudo ss -tulpen
If the output shows something similar to: LISTEN 0 128 0.0.0.0:22
it confirms that the SSH service (`sshd`) is running and listening on port **22**. Additionally, the ability to successfully connect to the EC2 instance via SSH using an SSH client is practical proof that the SSH service is active and accepting connections.

---

**3. Did you find any unexpected open ports? Explain briefly.**

No, I did not find any unexpected open ports. The scan showed only the expected services, such as **SSH on port 22** for remote administration and **HTTP on port 80** for serving the web application through Nginx. These ports are required for the server's intended functionality, and no unnecessary or suspicious ports were found open, which indicates that the server's exposed services are limited and follow good security practices.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

<img width="1720" height="472" alt="image" src="https://github.com/user-attachments/assets/c3198ca2-eb96-45e2-8152-f705e2448ee4" />


---

#### Screenshot 2 — Output of `sudo nginx -t`

<img width="882" height="131" alt="image" src="https://github.com/user-attachments/assets/81a4bb6f-f8b9-48a5-87f7-59bb04f61e01" />


---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

<img width="1872" height="196" alt="image" src="https://github.com/user-attachments/assets/2ad476fa-fe0e-4c73-b859-c0e534f00ec5" />


---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart in a production environment, the web application or website may become unavailable to users because the web server is not running to handle incoming HTTP requests. This can result in downtime, failed user requests, and potential business impact. Before restarting Nginx, it is good practice to validate the configuration using `sudo nginx -t` to detect any syntax errors. Monitoring tools and logs should also be checked to identify the root cause and restore the service as quickly as possible.

---

**2. What's your basic rollback plan?**

My basic rollback plan is to first identify the cause of the failure by checking the Nginx configuration with `sudo nginx -t` and reviewing the Nginx logs. If the issue was introduced by a recent deployment or configuration change, I would restore the previous working Nginx configuration and redeploy the last known stable version of the application. After confirming the configuration is valid, I would restart Nginx and verify that the website is accessible. This approach minimizes downtime and allows the service to be restored quickly while the root cause is investigated.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

<img width="1905" height="836" alt="image" src="https://github.com/user-attachments/assets/70d4808b-d50e-4365-a69a-69e04b6b7ad1" />


---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

<img width="1907" height="902" alt="image" src="https://github.com/user-attachments/assets/0ebec612-228b-458b-8194-962d9ca20d8a" />


---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

<img width="1782" height="371" alt="image" src="https://github.com/user-attachments/assets/7b5ee750-0ea7-4c8a-9d47-fb5b3f331f9d" />


---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

Yes, there were a few errors and warnings in the Nginx error log.

**Example 1:** open() "/usr/share/nginx/html/web/index.html" failed (2: No such file or directory)
**Explanation:** This means a client requested the `/web/` path, but the corresponding `index.html` file did not exist in the Nginx document root. As a result, Nginx returned a "file not found" error.

**Example 2:** open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory)
**Explanation:** This indicates that a browser requested the website's `favicon.ico` file, but it was not present in the document root. This is a common and generally non-critical error unless a favicon is expected.

Additionally, the log contained warnings such as: conflicting server name "_" on 0.0.0.0:80, ignored
This warning indicates that multiple Nginx server blocks were configured with the same default server name (`_`) on port 80. Nginx ignored one of the conflicting configurations, so the server configuration should be reviewed to remove the duplicate definition.

---

**2. If there were no errors, what does that indicate about the system?**
If there were no errors in the Nginx error log, it would indicate that Nginx is operating normally and has not encountered any recent issues while processing requests. This generally suggests that the server configuration is valid, the required files are available, and client requests are being handled successfully. While an empty or clean error log is a good sign of system health, it should still be verified with access logs and application testing to confirm that the website is functioning correctly.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes, my `curl` requests were visible in the Nginx access logs. This confirms that the HTTP requests successfully reached the Nginx web server and were processed. Seeing the requests in the access log proves that the network path, EC2 Security Group, and Nginx service were all functioning correctly, allowing traffic to flow from the client to the web server. It also verifies that Nginx was actively receiving and responding to incoming HTTP requests.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

<img width="726" height="47" alt="image" src="https://github.com/user-attachments/assets/f9b4800f-9064-494b-b31e-b9ad9a76545f" />


---

#### Screenshot 2 — Output of `free -h`

<img width="967" height="90" alt="image" src="https://github.com/user-attachments/assets/4c490577-5ef4-4b35-837e-1c8cd1ee865b" />


---

#### Screenshot 3 — Output of `df -h`

<img width="797" height="222" alt="image" src="https://github.com/user-attachments/assets/c448d694-f7f2-43ae-9beb-7eade1a1de7c" />


---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

<img width="837" height="486" alt="image" src="https://github.com/user-attachments/assets/b29fa4c4-e2f1-47dd-80c9-fed083ec00df" />


---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Based on the available outputs, memory is the resource that requires the closest monitoring. The system has 912 MB of RAM, with 240 MB used, 352 MB free, and about 502 MB available. While there is still sufficient available memory and the server is not under memory pressure, the total RAM is relatively small for a production server, so memory usage could become a bottleneck as application load increases.
The CPU/load is healthy, with a load average of 0.00, indicating the processor is idle. Disk usage is also healthy, with only 31% of the 8 GB root filesystem in use, leaving approximately 5.6 GB of free space.

---

**2. What happens if disk becomes 100% full in a production server?**

If the disk reaches 100% capacity, the server can experience serious issues. Applications may fail to write logs, upload files, or create temporary files, causing services such as Nginx or databases to malfunction or stop working. System updates, deployments, and even user logins may fail because the operating system cannot create new files. To prevent downtime, disk usage should be monitored regularly, and unnecessary files or old logs should be cleaned up before the disk becomes full.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

<img width="1145" height="307" alt="image" src="https://github.com/user-attachments/assets/bcf5a2f3-bf3c-402d-beea-690b2d3b2343" />

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

<img width="1917" height="905" alt="image" src="https://github.com/user-attachments/assets/19029e71-c13e-42d9-a5f2-b936420257ab" />


---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

<img width="1116" height="72" alt="image" src="https://github.com/user-attachments/assets/71786c12-baf4-40dc-8ebb-d809551e36d1" />

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

I confirm the correct application version by comparing the deployed build with the expected release version, Git commit, build timestamp, or deployment marker. I also check the files under /var/www/html, verify their modification times or checksums, and open the website to confirm the latest features and content are visible.

For example:
ls -lah /var/www/html
grep -R "version" /var/www/html 2>/dev/null | head
curl http://localhost

For a reliable production process, the application should display or store a clear version identifier, such as the Git commit hash or build number. The uploaded build content appears to be compiled React application code, so searching for a human-readable version will only work if one was included during the build.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

<img width="815" height="85" alt="image" src="https://github.com/user-attachments/assets/d36bcfdc-0902-48ce-95b5-36fbc13850db" />

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

<img width="815" height="85" alt="image" src="https://github.com/user-attachments/assets/3ae09e12-d175-4e55-8b6b-6061c7b67181" />

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

<img width="862" height="227" alt="image" src="https://github.com/user-attachments/assets/fa3e2c52-7578-414e-a8d3-9bc702f7ea14" />


---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

Nginx warning: nginx: **[warn] conflicting server name "_" on 0.0.0.0:80, ignored**

This occurred because multiple server blocks were configured to listen on port 80 with the same server_name _;, causing Nginx to ignore one of the configurations. It is a warning rather than a syntax error.


---

**2. How did you fix the issue?**

Executed: sudo nginx -t
to validate the Nginx configuration. The syntax was correct despite the warning.

Verified successful deployment from the response:
HTTP/1.1 200 OK
Server: nginx/1.30.3
Content-Type: text/html
This confirmed that Nginx was serving the application successfully.

The remaining Nginx warning can be resolved by removing or modifying the duplicate server_name _; configuration so that only one default server listens on port 80.

---

**3. How can you avoid this kind of issue in real production systems?**

Validate every configuration before deployment:
sudo nginx -t
Keep only one default server (server_name _;) per port to avoid configuration conflicts.
Use unique domain names or hostnames for each virtual host instead of multiple identical server_name _; entries.
Avoid copying placeholder characters (such as < >) from documentation directly into terminal commands.

After every deployment, verify the application using:
curl -I http://<server-ip-or-domain>
(Replace <server-ip-or-domain> with the actual IP or domain, without angle brackets.)

Include configuration validation (nginx -t) and smoke tests in the deployment pipeline before restarting Nginx to prevent production issues.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

<img width="862" height="239" alt="image" src="https://github.com/user-attachments/assets/e6bab662-c3c4-4419-9645-1d258a5d2396" />


---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

<img width="862" height="239" alt="image" src="https://github.com/user-attachments/assets/25038d19-7774-4cf9-8f4b-586b59f0d247" />


---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

The application likely broke because of an incorrect Nginx configuration or deployment change, such as a duplicate server block, an incorrect document root, missing build files, or an invalid command. The earlier warning about a conflicting server_name "_" shows that more than one Nginx configuration was trying to handle port 80, which could cause the wrong server block to be used.

The screenshot only shows the restored state with HTTP/1.1 200 OK, so it does not prove the exact original failure cause.

---

**2. How did you fix the issue and restore the application?**

I checked the Nginx configuration using:

sudo nginx -t

I corrected the configuration and ensured Nginx pointed to the correct React build directory. I then restarted or reloaded Nginx and tested the application using:

curl -I http://43.204.101.217

The response:

HTTP/1.1 200 OK

confirmed that Nginx was running and serving the application successfully again.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

I would validate every Nginx change with nginx -t before reloading it, keep backups of the last working configuration and application build, and avoid duplicate server blocks on the same port. I would also use automated deployment checks, health monitoring, log alerts, versioned releases, and a rollback process so the previous stable version can be restored quickly if a deployment fails.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

Write your answer here.

---

**2. Why should only required ports be open on a production server?**

Write your answer here.

---

**3. Why is it important for Nginx to be enabled on boot?**

Write your answer here.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Write your answer here.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Write your answer here.

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

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
- [ ] No sensitive data exposed

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
