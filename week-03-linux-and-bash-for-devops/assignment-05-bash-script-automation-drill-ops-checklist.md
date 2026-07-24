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

<<<<<<< HEAD
<img width="872" height="197" alt="image" src="https://github.com/user-attachments/assets/220d379a-6c48-45e7-90ae-775f197baf22" />


#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="732" height="182" alt="image" src="https://github.com/user-attachments/assets/915c2749-eac6-44d4-bda1-c638c21eeb81" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is Bash?**

<<<<<<< HEAD
Bash (Bourne Again Shell) is a Unix/Linux command-line interpreter and scripting language. It allows users to execute commands, automate repetitive tasks, manage files, and write scripts to simplify system administration and application deployment.

**2. What is the difference between shell and Bash?**

A shell is a program that provides an interface between the user and the operating system. Bash is a specific type of shell and one of the most widely used shells on Linux systems. While there are several shells such as sh, ksh, csh, and zsh, Bash offers additional features like command history, tab completion, aliases, and advanced scripting capabilities.

**3. Why is it important to confirm the Bash version before writing scripts?**

Confirming the Bash version ensures that the features and syntax used in a script are supported on the target system. Some commands and scripting features are only available in newer Bash versions, so checking the version helps avoid compatibility issues and ensures the script runs correctly across different environments.
=======
Add your answer here.

---

**2. What is the difference between shell and Bash?**

Add your answer here.

---

**3. Why is it important to confirm the Bash version before writing scripts?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<<<<<<< HEAD
<img width="812" height="197" alt="image" src="https://github.com/user-attachments/assets/10f10961-f87d-4340-bb9a-ca602771be48" />


#### Screenshot 2 — Output of `./first-script.sh`

<img width="792" height="126" alt="image" src="https://github.com/user-attachments/assets/ceb2a380-d2ef-4445-be3b-62f6469274cf" />


#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="845" height="71" alt="image" src="https://github.com/user-attachments/assets/864dff3b-177c-40df-89fb-96a143368013" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output of `./first-script.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

<<<<<<< HEAD
The #!/bin/bash line, called the shebang, tells the operating system to use the Bash shell to execute the script. It ensures the script runs with the correct interpreter, even if a different shell is the default on the system.

**2. Why do we use `chmod +x` before running a script?**

The chmod +x command gives a script execute permission. Without this permission, the operating system will not allow the script to be run directly as a program.

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

A) ./script.sh runs the script as an executable file. The script must have execute permission (chmod +x), and the shebang (#!/bin/bash) determines which interpreter is used.
B) bash script.sh explicitly runs the script using the Bash interpreter. It does not require the script to have execute permission, as long as the file is readable.
=======
Add your answer here.

---

**2. Why do we use `chmod +x` before running a script?**

Add your answer here.

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

<<<<<<< HEAD
<img width="887" height="292" alt="image" src="https://github.com/user-attachments/assets/4994dffb-2fd0-4abc-a543-2cfefd220a4d" />


#### Screenshot 2 — Output of `./user-info.sh`

<img width="917" height="172" alt="image" src="https://github.com/user-attachments/assets/60fb9733-2cf8-4def-8944-5eed5c7dad14" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output of `./user-info.sh`

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

<<<<<<< HEAD
A variable in Bash is a named container used to store data, such as text, numbers, or command output. It allows you to reuse values throughout a script, making the script easier to read, maintain, and update.

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash requires variable assignments to have no spaces around the = sign. If spaces are added, Bash treats the variable name, =, and value as separate commands or arguments, which results in a syntax error.

**3. How do you access the value stored inside a Bash variable?**

To access the value of a Bash variable, place a dollar sign ($) before the variable name. For example, if the variable is name, you can display its value using echo $name.
=======
Add your answer here.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Add your answer here.

---

**3. How do you access the value stored inside a Bash variable?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

<<<<<<< HEAD
<img width="905" height="382" alt="image" src="https://github.com/user-attachments/assets/b7f26f13-ec4c-48f2-b922-fe680eff4c78" />


#### Screenshot 2 — Output of `./tools-checklist.sh`

<img width="892" height="272" alt="image" src="https://github.com/user-attachments/assets/81956fb3-c437-4b5f-96c1-af3680924686" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

<<<<<<< HEAD
An array in Bash is a variable that can store multiple values under a single name. Each value is stored at a different index, making it easy to organize and work with related data.

**2. Why are arrays useful in scripts?**

Arrays are useful because they allow you to manage multiple related values without creating separate variables for each one. They make scripts more organized and are especially helpful when processing lists of files, users, servers, or other items.

**3. What does `"${tools[@]}"` mean?**

"${tools[@]}" refers to all the elements stored in the tools array. It expands each element individually while preserving spaces within each value, making it the preferred way to loop through every item in a Bash array.

**4. What is the purpose of the `for` loop in this script?**

The for loop is used to process each element in the array one by one. It repeats the same set of commands for every item, which makes the script efficient and avoids writing repetitive code.
=======
Add your answer here.

---

**2. Why are arrays useful in scripts?**

Add your answer here.

---

**3. What does `"${tools[@]}"` mean?**

Add your answer here.

---

**4. What is the purpose of the `for` loop in this script?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

<<<<<<< HEAD
<img width="816" height="307" alt="image" src="https://github.com/user-attachments/assets/72384693-7046-43b4-9f17-d28563ba511f" />


#### Screenshot 2 — Output of `./counter.sh`

<img width="792" height="220" alt="image" src="https://github.com/user-attachments/assets/5f27dcbc-37ae-4856-b34c-436925a6b2f1" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output of `./counter.sh`

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is a loop?**

<<<<<<< HEAD
A loop is a programming construct that repeatedly executes a block of code until a specified condition is met or for a fixed number of iterations. It helps automate repetitive tasks.

**2. Why do we use loops in Bash scripting?**

Loops are used in Bash scripting to perform the same operation multiple times without writing duplicate code. They make scripts shorter, easier to maintain, and more efficient when working with multiple files, users, or commands.

**3. How many times did the loop run in your script?**

The loop ran 5 times, once for each iteration specified in the script.

**4. What would you change if you wanted the loop to run 10 times?**

I would modify the loop's range or condition to iterate 10 times.
=======
Add your answer here.

---

**2. Why do we use loops in Bash scripting?**

Add your answer here.

---

**3. How many times did the loop run in your script?**

Add your answer here.

---

**4. What would you change if you wanted the loop to run 10 times?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

<<<<<<< HEAD
<img width="911" height="136" alt="image" src="https://github.com/user-attachments/assets/57b87350-e358-4115-b1ed-98fc9519c8e8" />


#### Screenshot 2 — Content of `file-check.sh`

<img width="871" height="530" alt="image" src="https://github.com/user-attachments/assets/7f754966-caa2-4505-b8c2-7d2e97a992ed" />


#### Screenshot 3 — Output of `./file-check.sh`

<img width="887" height="110" alt="image" src="https://github.com/user-attachments/assets/ae11f08c-249c-4194-9241-2f2e717f0603" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Content of `file-check.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `./file-check.sh`

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

<<<<<<< HEAD
The -d option checks whether a given path exists and is a directory. It returns true if the directory exists; otherwise, it returns false.

**2. What does `-f` check in Bash?**

The -f option checks whether a given path exists and is a regular file. It returns true only if the file exists and is not a directory or another special file type.

**3. Why should file and directory paths be stored in variables?**

Storing file and directory paths in variables makes scripts easier to read, update, and maintain. If a path changes, you only need to update the variable instead of modifying every occurrence in the script.

**4. What happens if the file does not exist?**

If the file does not exist, a condition using -f evaluates to false. The script can then execute an alternative action, such as displaying an error message, skipping the operation, or creating the file if needed.
=======
Add your answer here.

---

**2. What does `-f` check in Bash?**

Add your answer here.

---

**3. Why should file and directory paths be stored in variables?**

Add your answer here.

---

**4. What happens if the file does not exist?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

<<<<<<< HEAD
<img width="881" height="332" alt="image" src="https://github.com/user-attachments/assets/ebf68f2b-e865-4a60-b60e-d87ac301fcf3" />


#### Screenshot 2 — Output showing `Result: Pass`

<img width="951" height="107" alt="image" src="https://github.com/user-attachments/assets/0f8ba13f-8210-484c-8a67-a6541c2357a0" />


#### Screenshot 3 — Content of `score-check.sh` with `score=55`

<img width="871" height="352" alt="image" src="https://github.com/user-attachments/assets/2244d475-51f5-4ebf-b3fe-2c09cfb3e7ce" />



#### Screenshot 4 — Output showing `Result: Retry`

<img width="862" height="82" alt="image" src="https://github.com/user-attachments/assets/221eec60-e74d-4efe-b42e-b57e034b07ee" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output showing `Result: Pass`

Add your screenshot here.

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

Add your screenshot here.

---

#### Screenshot 4 — Output showing `Result: Retry`

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

<<<<<<< HEAD
The if-else statement is used to make decisions in a Bash script. It checks whether a condition is true or false and executes different blocks of code based on the result.

**2. What does `-ge` mean?**

The -ge operator means greater than or equal to. It is used to compare two integer values in a conditional statement.

**3. Why should conditions be tested with different values?**

Testing conditions with different values helps verify that the script behaves correctly in all scenarios. It ensures both the true and false branches work as expected and helps identify logic errors before the script is used in production.

**4. How can conditionals help in automation scripts?**

Conditionals allow automation scripts to make decisions based on system state or user input. They can perform different actions depending on whether a file exists, a service is running, a command succeeds, or a specific condition is met, making scripts more reliable and flexible.
=======
Add your answer here.

---

**2. What does `-ge` mean?**

Add your answer here.

---

**3. Why should conditions be tested with different values?**

Add your answer here.

---

**4. How can conditionals help in automation scripts?**

Add your answer here.

---
>>>>>>> upstream/main

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

<<<<<<< HEAD
<img width="737" height="807" alt="image" src="https://github.com/user-attachments/assets/7b100e14-9523-43f6-b6b7-25031b2fa4fa" />


#### Screenshot 2 — Output of `./final-automation.sh`

<img width="941" height="396" alt="image" src="https://github.com/user-attachments/assets/96d3e2ee-6465-42dc-93c0-897ff4e6ef90" />


#### Screenshot 3 — Output of `ls -lah` showing all created scripts

<img width="761" height="242" alt="image" src="https://github.com/user-attachments/assets/49dff57a-8d01-4394-b970-6d968edf2aa4" />

=======
Add your screenshot here.

---

#### Screenshot 2 — Output of `./final-automation.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

Add your screenshot here.

---
>>>>>>> upstream/main

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

<<<<<<< HEAD
A function in Bash is a reusable block of code that performs a specific task. Instead of writing the same commands multiple times, you can define them once in a function and call the function whenever needed.

**2. Why are functions useful in scripts?**

Functions make scripts more organized, reusable, and easier to maintain. They reduce duplicate code, improve readability, and simplify updates because changes only need to be made in one place.

**3. Which functions did you create in this script?**

I created functions to perform specific tasks, such as displaying messages, checking conditions, and organizing the script's workflow. Each function handled a separate task, making the script modular and easier to understand.

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script stores information in variables, manages multiple values using arrays, processes each item with loops, uses conditionals to make decisions based on different situations, performs operations on files and directories, and organizes related commands into functions. Together, these features create a structured, efficient, and reusable Bash script that automates tasks effectively.
=======
Add your answer here.

---

**2. Why are functions useful in scripts?**

Add your answer here.

---

**3. Which functions did you create in this script?**

Add your answer here.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

Add your answer here.

---
>>>>>>> upstream/main

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

<<<<<<< HEAD
https://www.linkedin.com/posts/muneer-ahmed-25322b206_devops-linux-bash-activity-7486318845519986688-naOq?utm_source=share&utm_medium=member_desktop&rcm=ACoAADRb5Z8BfmU5GnTuVjG5eHP-d8cMT-AYl0c

#### Screenshot — Published LinkedIn post

<img width="677" height="877" alt="image" src="https://github.com/user-attachments/assets/e6b0d874-0cc2-495d-9f03-b6e57550e394" />

=======
`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---
>>>>>>> upstream/main

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

<<<<<<< HEAD
- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
=======
- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
>>>>>>> upstream/main
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

<<<<<<< HEAD
*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
=======
*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
>>>>>>> upstream/main
