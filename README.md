# 🚀 User Guide: Automating Terraform with GitHub Actions

This guide provides a step-by-step approach to setting up, using, and managing **Terraform with GitHub Actions** for infrastructure automation.

---

## 📌 Table of Contents

- [📖 Introduction](#introduction)
- [🔧 Prerequisites](#prerequisites)
- [⚙️ Setting Up the Project](#setting-up-the-project)
- [🤖 Understanding GitHub Actions Workflow](#understanding-github-actions-workflow)
- [📌 Managing Infrastructure with Terraform](#managing-infrastructure-with-terraform)
- [🗑️ Destroying Resources](#destroying-resources)
- [🔧 Troubleshooting & FAQs](#troubleshooting--faqs)
- [📚 References](#references)

---

## 📖 Introduction

This project automates **Terraform deployments** using **GitHub Actions**. Every time you push code changes to the repository, Terraform automatically runs and applies changes to your AWS infrastructure.

With this setup, you can:
✅ Manage AWS infrastructure as **code**  
✅ Automate deployment using **GitHub Actions**  
✅ Ensure infrastructure consistency with **Terraform state management**  

---

## 🔧 Prerequisites

Before you begin, make sure you have:

- **Git & GitHub**
  - Install [Git](https://git-scm.com/downloads)
  - A **GitHub account**
- **AWS Account**
  - Create an **IAM User** with the following permissions:
    - `AmazonEC2FullAccess`
    - `AmazonVPCFullAccess`
    - `IAMFullAccess`
- **Terraform**
  - Install [Terraform](https://developer.hashicorp.com/terraform/downloads)
  - Verify installation:

    ```sh
    terraform version
    ```

---

## ⚙️ Setting Up the Project

### 1️⃣ Clone the Repository

```sh
git clone https://github.com/tiqsclass6/learn-terraform-github-actions.git
cd learn-terraform-github-actions
```

### 2️⃣ Set Up AWS Credentials in GitHub

1. **Go to your repository on GitHub**
2. Navigate to **Settings** > **Secrets and variables** > **Actions**
3. Click **New repository secret** and add:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`

### 3️⃣ Initialize Terraform

Run the following commands to initialize Terraform:

```sh
terraform init
```

This downloads necessary Terraform providers and sets up your local environment.

---

## 🤖 Understanding GitHub Actions Workflow

This project contains **GitHub Actions workflows** inside `.github/workflows/`:

| Workflow File          | Description                                          |
|------------------------|------------------------------------------------------|
| **terraform-plan.yml** | Runs `terraform plan` on every PR to preview changes. |
| **terraform-apply.yml** | Runs `terraform apply` on the `main` branch after merging a PR. |

### How It Works

#### 📌 **Pull Request Workflow**

- When you create a **Pull Request (PR)**, GitHub Actions runs `terraform plan` to **preview changes**.
- The Terraform plan is **commented on the PR**.

#### 📌 **Merge & Apply Workflow**

- When the PR is **merged to `main`**, GitHub Actions runs `terraform apply` to **deploy changes** automatically.

---

## 📌 Managing Infrastructure with Terraform

### 1️⃣ Making Infrastructure Changes

- Modify the Terraform configuration (`main.tf`, `variables.tf`, etc.).
- Stage and commit your changes:

  ```sh
  git add .
  git commit -m "Updated Terraform infrastructure"
  git push origin feature-branch
  ```

- Open a **Pull Request (PR)** in GitHub.

### 2️⃣ Reviewing Terraform Plan

- GitHub Actions will automatically **run `terraform plan`** and post the output as a comment on your PR.

### 3️⃣ Merging to Apply Changes

- Once the plan looks good, **merge the PR** into `main`.
- **Terraform Apply** runs automatically via GitHub Actions to provision the infrastructure.

---

## 🗑️ Destroying Resources

To **manually destroy** your infrastructure:

```sh
terraform destroy
```

This removes **all AWS resources** created by Terraform.

Alternatively, to disable **Terraform Apply** in GitHub Actions:

1. Navigate to **Settings** > **Actions** > **General**
2. Set **Workflow permissions** to **Read repository contents** only.

---

## 🔧 Troubleshooting & FAQs

### ❓ Terraform Apply Failed on GitHub Actions

✅ **Solution:** Check the Actions logs for errors. Common issues:

- Invalid AWS credentials (Check GitHub Secrets)
- Syntax errors in `main.tf`
- AWS quota exceeded

### ❓ How to Rollback Changes?

✅ **Solution:** Revert to a previous commit:

```sh
git revert HEAD~1
git push origin main
```

This triggers a new Terraform run that restores the previous state.

### ❓ How to Manually Run GitHub Actions?

✅ **Solution:**  

1. Go to **Actions** in your repository.  
2. Select the workflow (`terraform-apply.yml`).  
3. Click **Run Workflow**.

---

## 📚 References

- 📌 [Terraform Docs](https://developer.hashicorp.com/terraform/docs)
- 📌 [GitHub Actions](https://docs.github.com/en/actions)
- 📌 [AWS IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)

---
