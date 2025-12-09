# 🚀 Terraform Project: Deploy EC2 with PostgreSQL (Automated Setup)

This project demonstrates how to use **Terraform (Infrastructure as Code)** to automatically provision an **Ubuntu EC2 instance on AWS** and install **PostgreSQL database server** using a `user_data` automation script.  
This setup is created for **personal learning and hands-on DevOps practice** using Terraform and AWS.

---

## 📌 Project Objectives

- Create and manage AWS infrastructure using **Terraform**
- Provision an **Ubuntu EC2 instance**
- Configure security groups (SSH + PostgreSQL access)
- Automatically install and configure **PostgreSQL** on EC2 using `user_data`
- Store infrastructure state using Terraform state files
- Practice real DevOps workflows with infrastructure as code

---

## 🏗️ Architecture Overview

Local Terraform (Ubuntu/Linux)
|
v
AWS Cloud
┌────────────────────────────┐
│ EC2 Instance (Ubuntu) │
│ - PostgreSQL installed │
│ - user_data automation │
│ - SSH enabled (Port 22) │
└────────────────────────────┘
│ Security Group Rules │
│ - Allow SSH (22) │
│ - Allow PostgreSQL (5432)│
└────────────────────────────┘

yaml
Copy code

---

## 📎 Technologies Used

| Tool / Service | Purpose |
|----------------|---------|
| Terraform | Infrastructure as Code |
| AWS EC2 | Compute to host PostgreSQL |
| Ubuntu | OS on EC2 |
| PostgreSQL | Database Server |
| AWS Security Groups | Network access control |

---

## 📁 Project Structure

ec2-rds-terraform-demo/
│
├── main.tf # EC2 + Security Groups + PostgreSQL installation
├── variables.tf # Variable definitions
├── terraform.tfvars # Variable values (Not committed to GitHub)
├── outputs.tf # Outputs (Public IP / DNS)
└── .gitignore # To avoid sensitive files being pushed

yaml
Copy code

---

## ⚙️ Prerequisites

Before running this project, ensure you have:

- AWS Account
- AWS CLI installed and configured (`aws configure`)
- Terraform installed (`terraform -version`)
- Ubuntu/Linux terminal
- SSH key generated in AWS (e.g., `terraform.pem`)

---

## 🚀 Deploy Instructions

Run these commands inside the project directory:

```bash
terraform init
terraform fmt
terraform validate
terraform apply
Enter yes when prompted.

🔑 Connect to EC2
After applying, get the public IP:

bash
Copy code
terraform output ec2_public_ip
SSH into the EC2 instance:

bash
Copy code
chmod 400 terraform.pem
ssh -i terraform.pem ubuntu@<ec2_public_ip>
🗄️ Verify PostgreSQL Installation
Inside EC2:

bash
Copy code
psql --version
sudo systemctl status postgresql
(Optional) Connect to DB:

bash
Copy code
psql -U appuser -d appdb -h localhost
🔐 Security & GitHub Best Practices
⚠️ Never commit sensitive files!

Make sure .gitignore includes:

markdown
Copy code
*.tfstate
terraform.tfvars
.terraform/
*.pem
🎯 Learning Outcome
By completing this project, you will understand:

✔ Infrastructure as Code (IaC)
✔ Provisioning with Terraform
✔ Automating configuration with user_data
✔ Working with AWS EC2 + Security Groups
✔ Real DevOps workflow (version control + GitHub)
