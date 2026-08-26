\# Cloud Infrastructure Provisioning Platform



A self-service cloud infrastructure provisioning platform built with Python, FastAPI, Terraform, and AWS.



The **Cloud Infrastructure Provisioning Platform** is basically a **self-service tool for creating cloud infrastructure automatically**.

Instead of a developer/engineer manually going into AWS and creating VPCs, EC2 instances, security groups, IAM roles, etc., they use your platform to request what they need, and your system provisions it using **Terraform**.

### Simple example

Imagine a developer needs a development environment.

Normally, they might have to ask a DevOps engineer:

> "Can you create an EC2 instance, networking, security group and IAM role for my application?"

Your platform changes that.

They open your application and select:

```text
Application: Resume Tracker
Environment: Development
Cloud: AWS
Region: ap-south-1
Instance Type: t3.micro
Database: PostgreSQL
```

Then click:

**Provision Infrastructure**

Your system does:

```text
User
  ↓
Your Web UI / API
  ↓
FastAPI Backend
  ↓
Validate Request
  ↓
Generate/Select Terraform Configuration
  ↓
Terraform Plan
  ↓
Terraform Apply
  ↓
AWS
  ↓
Infrastructure Created
```

The user then gets something like:

```text
Provisioning: SUCCESS

Environment: Development

Resources:
✓ VPC
✓ Subnet
✓ Security Group
✓ EC2 Instance
✓ IAM Role
✓ PostgreSQL Database

Status: Running
```

---

# What exactly would your platform manage?

You don't need to support everything AWS offers.

Start with a small set.

### Networking

Your platform can create:

* VPC
* Public/private subnet
* Internet Gateway
* Route tables
* Security groups

### Compute

For example:

* EC2

Later:

* ECS
* EKS

### Storage

* S3

### Database

* RDS PostgreSQL

### IAM

* IAM roles
* IAM policies

So a user could request:

> "Create a development environment for my application."

And your platform creates the required infrastructure.

---

# Why Terraform is important

This is the core of the project.

Your FastAPI application shouldn't manually execute dozens of AWS API calls.

Instead:

```text
FastAPI
   ↓
Terraform configuration
   ↓
Terraform
   ↓
AWS
```

Terraform becomes your **Infrastructure as Code engine**.

For example, your platform might have Terraform modules like:

```text
terraform/
├── modules/
│   ├── vpc/
│   ├── ec2/
│   ├── rds/
│   ├── s3/
│   └── iam/
│
└── environments/
    ├── dev/
    ├── staging/
    └── prod/
```

Your application decides what the user requested, and Terraform handles actually creating the infrastructure.

---

# What happens when someone wants to delete it?

Your platform should also support:

**Destroy Environment**

For example:

```text
Resume Tracker - DEV
        ↓
    Destroy
        ↓
Terraform Destroy
        ↓
AWS Resources Removed
```

This is important because otherwise you'll create resources and forget about them, which can generate AWS bills.

---

# You can also add a dashboard

A simple dashboard could show:

```text
Cloud Infrastructure Platform

Environments
─────────────────────────────

resume-tracker-dev
AWS | ap-south-1
Status: Running

sales-agent-dev
AWS | ap-south-1
Status: Running


Resources
─────────────────────────────

EC2          3
VPC          2
S3           4
RDS          1
IAM Roles    6
```

You don't need an amazing frontend. Even a basic React interface or simple FastAPI UI is enough.

---

# Where CI/CD comes in

You can connect GitHub Actions.

For example:

```text
Developer pushes Terraform change
             ↓
       GitHub Actions
             ↓
    terraform fmt
             ↓
    terraform validate
             ↓
      terraform plan
             ↓
       Approval
             ↓
      terraform apply
```

Now your project isn't just:

> "I know Terraform."

You're demonstrating an actual **infrastructure delivery workflow**.

---

# Where Docker comes in

Your platform itself can be containerized:

```text
┌─────────────────────────┐
│       Docker            │
│                         │
│  ┌───────────────────┐  │
│  │ FastAPI           │  │
│  │ Provisioning API  │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

Then you can deploy that application to AWS.

---

# And Kubernetes?

This should be **Phase 2**, not the starting point.

Eventually:

```text
User
 ↓
FastAPI
 ↓
Docker
 ↓
Kubernetes / EKS
 ↓
AWS
```

You could run your provisioning platform itself inside Kubernetes.

But don't add Kubernetes just because "Kubernetes looks good on a resume."

First make the provisioning system work.

---

# The interesting part for your career

This project fits your profile unusually well.

Your Cognizant experience already involves things like:

**Cloud → IAM/RBAC → provisioning → incidents → AWS/Azure/GCP → Terraform**

This project lets you demonstrate the **engineering side** of that.

Your story becomes:

> **At work:** I support and troubleshoot cloud infrastructure.

> **In my project:** I built a system that automates cloud infrastructure provisioning using Terraform and AWS.

That's much stronger than having another generic Python project.

---

## What the finished project could ultimately demonstrate

**Python**
→ build the provisioning API

**FastAPI**
→ expose infrastructure operations

**AWS**
→ actual cloud infrastructure

**Terraform**
→ Infrastructure as Code

**IAM**
→ secure permissions

**Docker**
→ containerize the platform

**GitHub Actions**
→ CI/CD

**Kubernetes**
→ run the platform in a container orchestration environment

**PostgreSQL**
→ store provisioning requests/status/audit information

**Linux**
→ deployment and troubleshooting

So one project can legitimately demonstrate a large portion of the stack you're trying to move toward.

### But don't make it unnecessarily huge.

I'd build it in this order:

**MVP:** FastAPI + Terraform + AWS EC2/VPC/IAM
↓
**V2:** PostgreSQL + provisioning history + destroy operation
↓
**V3:** Docker + GitHub Actions
↓
**V4:** Terraform modules + dev/staging environments
↓
**V5:** Kubernetes/EKS

If you finish **V1–V3 properly**, you already have a worthwhile resume project. V4–V5 are what turn it into a strong portfolio piece.


