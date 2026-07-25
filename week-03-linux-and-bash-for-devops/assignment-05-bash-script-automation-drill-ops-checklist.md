# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

<img width="1167" height="257" alt="image" src="https://github.com/user-attachments/assets/2253290c-8075-412b-8cd6-0699222d4c72" />


---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="917" height="541" alt="image" src="https://github.com/user-attachments/assets/14abd8bc-baeb-461f-a73f-5669cd854e89" />

---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash (Bourne Again Shell) is a command-line interpreter that allows users to interact with the Linux operating system. It enables users to run commands, manage files, automate tasks, and create shell scripts to perform repetitive operations efficiently.

---

**2. What is the difference between shell and Bash?**

A shell is a general interface that allows users to communicate with the operating system. There are different types of shells, such as Bash, Zsh, Ksh, and Fish. Bash is one specific type of shell and is the default shell on many Linux systems. In simple terms, every Bash is a shell, but not every shell is Bash.

---

**3. Why is it important to confirm the Bash version before writing scripts?**

It is important to confirm the Bash version because different versions support different features and syntax. A script written for a newer Bash version may not work correctly on an older version. Checking the version helps ensure compatibility, prevents errors, and makes the script more reliable across different Linux systems.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<img width="1917" height="902" alt="image" src="https://github.com/user-attachments/assets/035d0d39-d2c3-4701-bffc-3206c461f811" />


---

#### Screenshot 2 — Output of `./first-script.sh`

<img width="1897" height="482" alt="image" src="https://github.com/user-attachments/assets/e19f78e7-2001-48c9-b4e9-3f90ee7864c3" />


---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="1917" height="227" alt="image" src="https://github.com/user-attachments/assets/f442dc05-f3b1-4a03-a5a2-a68024b3ddc3" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

#!/bin/bash is called the shebang line. It tells the operating system to use the Bash interpreter to execute the script, ensuring the commands run in the Bash shell.

---

**2. Why do we use `chmod +x` before running a script?**

The chmod +x command gives the script execute permission. Without this permission, the operating system will not allow the script to be run directly.

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

./script.sh runs the script as an executable file. The script must have execute permission (chmod +x) and usually starts with #!/bin/bash.
bash script.sh runs the script by explicitly calling the Bash interpreter. It does not require the script to have execute permission, but the file must be readable.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

<img width="681" height="267" alt="image" src="https://github.com/user-attachments/assets/1fc3dc5b-c2c0-4e50-bac3-73a4570e2653" />


---

#### Screenshot 2 — Output of `./user-info.sh`

<img width="687" height="150" alt="image" src="https://github.com/user-attachments/assets/e4899021-1e16-4c72-af8b-430557d983cb" />



---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a named container used to store data, such as text or numbers, so it can be reused throughout a script.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash requires variable assignments to have no spaces around the = sign. If spaces are added, Bash treats them as separate commands or arguments, causing an error.

---

**3. How do you access the value stored inside a Bash variable?**

You access the value of a Bash variable by placing a dollar sign ($) before the variable name. For example, if the variable is name, its value is accessed as $name.

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

<img width="1902" height="427" alt="image" src="https://github.com/user-attachments/assets/bdcf2a13-2098-4c96-9cdf-88fdefc3c70b" />


---

#### Screenshot 2 — Output of `./tools-checklist.sh`

<img width="1917" height="630" alt="image" src="https://github.com/user-attachments/assets/b1a8d088-08dc-4b32-8f7c-bfb6224f7da2" />


---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in Bash is a variable that stores multiple values under a single name.

---

**2. Why are arrays useful in scripts?**

Arrays make it easy to store and process multiple related values without creating separate variables for each one.

---

**3. What does `"${tools[@]}"` mean?**

"${tools[@]}" represents all the elements in the tools array, allowing the script to access each value one by one.

---

**4. What is the purpose of the `for` loop in this script?**

The for loop goes through each item in the array and performs the same action, such as printing each tool in the checklist.

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

<img width="1915" height="422" alt="image" src="https://github.com/user-attachments/assets/4175f484-257f-4ca7-80cd-ad533d0f91de" />


---

#### Screenshot 2 — Output of `./counter.sh`

<img width="1917" height="667" alt="image" src="https://github.com/user-attachments/assets/def2453a-124c-4406-8d9f-a43d81124068" />


---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming structure that repeats a set of commands until a specified condition or number of repetitions is completed.

---

**2. Why do we use loops in Bash scripting?**

Loops help automate repetitive tasks and reduce the need to write the same commands multiple times.

---

**3. How many times did the loop run in your script?**

The loop ran 10 times, once for each number from 1 to 10.

---

**4. What would you change if you wanted the loop to run 10 times?**

The script already runs 10 times because it uses: {1..10}

To change the number of repetitions, update the ending number. For example, {1..20} would run the loop 20 times.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

<img width="1912" height="352" alt="image" src="https://github.com/user-attachments/assets/476110c1-ad82-4c1e-a30a-a44ba7b34951" />


---

#### Screenshot 2 — Content of `file-check.sh`

<img width="1917" height="687" alt="image" src="https://github.com/user-attachments/assets/f5cb1ab1-fa62-465a-a49d-1f793575d326" />


---

#### Screenshot 3 — Output of `./file-check.sh`

<img width="1917" height="330" alt="image" src="https://github.com/user-attachments/assets/ef09049a-7a04-4319-af86-c8e60d1ff300" />


---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

-d checks whether a directory exists at the specified path.

---

**2. What does `-f` check in Bash?**

-f checks whether a regular file exists at the specified path.

---

**3. Why should file and directory paths be stored in variables?**

Storing paths in variables makes the script easier to read, update, and reuse without changing the same path in multiple places.

---

**4. What happens if the file does not exist?**

If the file does not exist, the condition evaluates to false, and the script executes the else block, displaying a message that the file was not found.

---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

<img width="1907" height="387" alt="image" src="https://github.com/user-attachments/assets/2d7edb33-5354-4183-8bde-a669ab8d6e20" />


---

#### Screenshot 2 — Output showing `Result: Pass`

<img width="1917" height="225" alt="image" src="https://github.com/user-attachments/assets/c04c1e45-bd7d-4415-ba71-410aa8652aef" />


---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

<img width="1917" height="377" alt="image" src="https://github.com/user-attachments/assets/f9814bcc-f07a-414b-9506-4c15af702352" />


---

#### Screenshot 4 — Output showing `Result: Retry`

<img width="1907" height="257" alt="image" src="https://github.com/user-attachments/assets/86cc506a-42b8-43b3-9c53-cece4f206c2c" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

The if-else statement allows a script to make decisions by running different commands based on whether a condition is true or false.

---

**2. What does `-ge` mean?**

-ge means greater than or equal to. It is used to compare two numeric values.

---

**3. Why should conditions be tested with different values?**

Testing different values helps verify that the script behaves correctly in all situations and produces the expected output.

---

**4. How can conditionals help in automation scripts?**

Conditionals allow automation scripts to make decisions automatically, such as checking files, validating input, or performing different actions based on specific conditions.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

<img width="1917" height="941" alt="image" src="https://github.com/user-attachments/assets/6639f1ab-c074-44ed-ac1b-2071e844faed" />


---

#### Screenshot 2 — Output of `./final-automation.sh`

<img width="1917" height="602" alt="image" src="https://github.com/user-attachments/assets/a5b59199-bdf9-4f97-be95-2112b0da738d" />


---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

<img width="1917" height="447" alt="image" src="https://github.com/user-attachments/assets/caf50fe5-b60b-47ef-a22e-028a103bd955" />


---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function in Bash is a named group of commands that performs a specific task. It can be called whenever that task needs to run.

---

**2. Why are functions useful in scripts?**

Functions make scripts easier to organize, read, reuse, and maintain. They also prevent the same commands from being written repeatedly.

---

**3. Which functions did you create in this script?**

The script contains four functions:

show_user_info
show_tools
check_score
check_file

Each function handles a separate part of the automation.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script uses variables to store the name, score, and file path. It uses an array to store tool names and a loop to print each tool. Conditionals check the score and whether the file exists. Functions organize these tasks into reusable sections.

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
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
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
