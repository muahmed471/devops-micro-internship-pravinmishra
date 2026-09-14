# Assignment 1 — Create an Azure Virtual Machine using Terraform

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will use Terraform to provision a complete Azure Virtual Machine environment, including a resource group, virtual network, subnet, public IP, network interface, and a Linux-based virtual machine. You will set up and verify the required local tools, define the infrastructure in Terraform, initialize the project, review and apply the plan, verify the running VM through Azure CLI, capture the public IP output, and destroy the resources after testing.

---

# Task 0 — Set Up and Verify the Terraform and Azure CLI Environment

## Goal

Prepare your local environment for Terraform deployment by installing Terraform, Azure CLI, and the HashiCorp Terraform extension in VS Code, signing in to your Azure account, and confirming that all required tools are working correctly.

### Evidence

#### Screenshot 1 — Terminal showing successful `terraform version` output

![screenshot](./screenshots/Assignment1_Screenshot0.png)

#### Screenshot 2 — Terminal showing successful `az version` output

![screenshot](./screenshots/Assignment1_Screenshot0a.png)

#### Screenshot 3 — VS Code Extensions panel showing the HashiCorp Terraform extension installed and enabled

![screenshot](./screenshots/Assignment1_Screenshot0b.png)

# Task 1 — Create a New Terraform Project and Define the Infrastructure

## Goal

Create a new Terraform project and define the complete Azure Virtual Machine environment in `main.tf` by using the official Terraform Registry documentation.

### Evidence

#### Screenshot 4 — VS Code showing the AzureRM provider configuration and resource group configuration in `main.tf`

![screenshot](./screenshots/Assignment1_Screenshot1.png)

#### Screenshot 5 — VS Code showing the Linux virtual machine configuration and public IP `output` block in `main.tf`. Ensure that the VM password is hidden or redacted

![screenshot](./screenshots/Assignment1_Screenshot2.png)

# Task 2 — Initialize Terraform

## Goal

Initialize the Terraform working directory and download the required provider components.

### Evidence

#### Screenshot 6 — Terminal showing the successful `terraform init` output

![screenshot](./screenshots/Assignment1_Screenshot3.png)

# Task 3 — Plan and Apply the Configuration

## Goal

Review the Terraform execution plan and provision the Azure resources.

### Evidence

#### Screenshot 7 — Terraform plan summary showing the proposed resources

![screenshot](./screenshots/Assignment1_Screenshot4.png)
![screenshot](./screenshots/Assignment1_Screenshot4a.png)
![screenshot](./screenshots/Assignment1_Screenshot4b.png)
![screenshot](./screenshots/Assignment1_Screenshot4c.png)

#### Screenshot 8 — Terraform apply output showing successful completion

![screenshot](./screenshots/Assignment1_Screenshot5.png)

#### Screenshot 9 — Terraform output showing the public IP address of the VM

![screenshot](./screenshots/Assignment1_Screenshot6.png)

# Task 4 — Verify the Deployment

## Goal

Confirm through Azure CLI that the virtual machine was created successfully and is currently running.

### Evidence

#### Screenshot 10 — Azure CLI output showing the deployed VM name and `VM running` status

![screenshot](./screenshots/Assignment1_Screenshot7.png)

# Task 5 — Destroy the Resources

## Goal

Remove all Azure resources created by Terraform after completing the deployment and verification.

### Evidence

#### Screenshot 11 — Terminal showing successful `terraform destroy` completion

![screenshot](./screenshots/Assignment1_Screenshot8.png)

### Notes

Write a short paragraph explaining what you learned or any issues you encountered.

I learned how to use Terraform to define, plan, deploy, verify, and destroy Azure infrastructure. I created an Azure resource group, virtual network, subnet, public IP, network interface, and Linux VM using Terraform. I also learned how Terraform state manages resources and how to troubleshoot deployment issues. One issue I encountered was that the Standard_B1s VM size was unavailable in the South India region, so I checked the available SKUs and changed the VM size to Standard_B2s_v2 before successfully deploying the VM.

# Submission Instructions

- Complete all tasks in sequence and include all required screenshots specified in Tasks 0–5.
- Do not expose passwords, keys, account IDs, or other sensitive information in screenshots.

---

# Completion Checklist

- [x] Task 1: `terraform-azure-vm` project created with all required resources defined (Screenshots 1–2)
- [x] Task 2: `terraform init` completed successfully (Screenshot 3)
- [x] Task 3: Plan reviewed and `terraform apply` completed, public IP recorded (Screenshots 4–6)
- [x] Task 4: VM verified as running via Azure CLI (Screenshot 7)
- [x] Task 5: `terraform destroy` completed successfully (Screenshot 8)
- [x] Learning/issues paragraph written (Notes)
- [x] No sensitive information exposed

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

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*