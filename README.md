# Terraform EC2 PostgreSQL — Automated Infrastructure Deployment

> Infrastructure as Code project demonstrating automated provisioning of an Ubuntu EC2 instance with PostgreSQL on AWS using Terraform.

---

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Technologies](#technologies)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Connecting to the Instance](#connecting-to-the-instance)
- [Verifying PostgreSQL](#verifying-postgresql)
- [Security & Best Practices](#security--best-practices)
- [Learning Outcomes](#learning-outcomes)

---

## Overview

This project uses **Terraform** to automate the provisioning of AWS infrastructure, including an Ubuntu EC2 instance with PostgreSQL pre-installed via a `user_data` bootstrap script. It is designed for hands-on DevOps learning, covering real-world workflows with Infrastructure as Code (IaC), AWS security groups, and version-controlled infrastructure management.

---

## Architecture

```
Local Machine (Terraform CLI)
          │
          ▼
    ┌─────────────────────────────────────┐
    │           AWS Cloud                 │
    │                                     │
    │   ┌─────────────────────────────┐   │
    │   │     EC2 Instance (Ubuntu)   │   │
    │   │  ─ PostgreSQL (auto-install)│   │
    │   │  ─ user_data bootstrap      │   │
    │   │  ─ SSH access (Port 22)     │   │
    │   └─────────────────────────────┘   │
    │                                     │
    │   ┌─────────────────────────────┐   │
    │   │       Security Group        │   │
    │   │  ─ Inbound: SSH (22)        │   │
    │   │  ─ Inbound: PostgreSQL(5432)│   │
    │   └─────────────────────────────┘   │
    └─────────────────────────────────────┘
```

---

## Technologies

| Tool / Service       | Purpose                          |
|----------------------|----------------------------------|
| Terraform            | Infrastructure as Code (IaC)     |
| AWS EC2              | Compute instance for PostgreSQL  |
| Ubuntu               | Operating system on EC2          |
| PostgreSQL           | Relational database server       |
| AWS Security Groups  | Network access control           |
| AWS CLI              | AWS credential configuration     |

---

## Project Structure

```
ec2-rds-terraform-demo/
│
├── main.tf              # EC2 instance, security groups, and user_data script
├── variables.tf         # Input variable definitions
├── terraform.tfvars     # Variable values (excluded from version control)
├── outputs.tf           # Output values (public IP, DNS)
└── .gitignore           # Excludes sensitive and generated files
```

---

## Prerequisites

Ensure the following are installed and configured before proceeding:

- [AWS Account](https://aws.amazon.com/)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) — configured via `aws configure`
- [Terraform](https://developer.hashicorp.com/terraform/install) — verify with `terraform -version`
- Ubuntu / Linux terminal
- An SSH key pair created in AWS (e.g., `terraform.pem`)

---

## Getting Started

Run the following commands from within the project directory:

```bash
# 1. Initialize the working directory and download providers
terraform init

# 2. Format configuration files
terraform fmt

# 3. Validate configuration syntax
terraform validate

# 4. Review the execution plan
terraform plan

# 5. Apply and provision infrastructure
terraform apply
```

> Enter `yes` when prompted to confirm the deployment.

---

## Connecting to the Instance

After a successful `terraform apply`, retrieve the public IP:

```bash
terraform output ec2_public_ip
```

SSH into the EC2 instance:

```bash
chmod 400 terraform.pem
ssh -i terraform.pem ubuntu@<ec2_public_ip>
```

---

## Verifying PostgreSQL

Once connected to the instance, verify the PostgreSQL installation:

```bash
# Check installed version
psql --version

# Confirm the service is running
sudo systemctl status postgresql
```

Optionally, connect to the database:

```bash
psql -U appuser -d appdb -h localhost
```

---

## Security & Best Practices

> ⚠️ **Never commit sensitive files to version control.**

Ensure your `.gitignore` includes the following:

```gitignore
# Terraform state files
*.tfstate
*.tfstate.backup

# Local variable values (may contain secrets)
terraform.tfvars

# Terraform working directory
.terraform/
.terraform.lock.hcl

# SSH private keys
*.pem
```

Additional recommendations:

- Restrict Security Group inbound rules to known IP ranges instead of `0.0.0.0/0`
- Rotate or revoke SSH key pairs after use in non-production environments
- Use Terraform remote state (e.g., S3 + DynamoDB) for team collaboration

---

## Learning Outcomes

By completing this project, you will gain practical experience with:

- **Infrastructure as Code (IaC)** — managing cloud resources declaratively with Terraform
- **EC2 Provisioning** — launching and configuring Ubuntu instances on AWS
- **Bootstrap Automation** — using `user_data` scripts for post-launch configuration
- **Network Security** — defining inbound/outbound rules with AWS Security Groups
- **DevOps Workflow** — version-controlled infrastructure with Git and GitHub
- **State Management** — understanding how Terraform tracks resource state

---

## Contributing

This project is intended for personal learning. Feel free to fork and adapt it for your own DevOps practice.

---

