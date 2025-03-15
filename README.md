# Learn Terraform with GitHub Actions  

## Step-by-Step Guide

## Overview

This repository demonstrates how to use **Terraform** in combination with **GitHub Actions** for automating infrastructure deployments. The repository is structured to facilitate Infrastructure as Code (IaC) principles while leveraging CI/CD automation with GitHub Actions.

---

## Step 1: Clone the Repository

Begin by cloning the repository to your local machine:

```sh
git clone https://github.com/tiqsclass6/learn-terraform-github-actions.git
cd learn-terraform-github-actions
```

**Impact:** This ensures you have the latest project code locally, allowing you to review the Terraform configurations and GitHub Actions workflows.

---

## Step 2: Install Required Tools

Ensure the following tools are installed:

- **Terraform**: Infrastructure as Code tool.
- **GitHub CLI (optional)**: For managing GitHub repositories from the command line.

Verify installations:

```sh
terraform -version  # Check Terraform version
gh --version        # Check GitHub CLI version (if installed)
```

**Impact:** Having these tools installed is necessary to execute Terraform commands locally and interact with GitHub.

---

## Step 3: Configure GitHub Secrets for Terraform Authentication

For Terraform to deploy infrastructure through GitHub Actions, you need to set up **GitHub Secrets**.

1. Navigate to your repository on GitHub.
2. Go to **Settings** > **Secrets and variables** > **Actions**.
3. Add the following secrets:

   - `AWS_ACCESS_KEY_ID`: AWS credentials for Terraform deployments.
   - `AWS_SECRET_ACCESS_KEY`: AWS secret key for Terraform.
   - `TF_CLOUD_ORG`: Terraform Cloud organization name (if using Terraform Cloud).
   - `TF_API_TOKEN`: Terraform API token (if using Terraform Cloud).

**Impact:** These secrets allow the GitHub Actions workflow to authenticate and execute Terraform commands securely.

---

## Step 4: Understand the GitHub Actions Workflows

The **GitHub Actions workflow files** located in `.github/workflows/` automate various Terraform-related processes. The key workflows include:

### `terraform-plan.yml`

1. **Checkout Code**: Fetches the repository contents.
2. **Setup Terraform**: Installs Terraform on the runner.
3. **Terraform Format & Validate**: Ensures Terraform code syntax follows best practices.
4. **Terraform Plan**: Generates a dry-run execution plan for review before deployment.

### `terraform-apply.yml`

1. **Checkout Code**: Fetches the repository contents.
2. **Setup Terraform**: Installs Terraform on the runner.
3. **Terraform Apply**: Executes the Terraform plan to deploy infrastructure after manual approval.

**Impact:** These workflows ensure automation, security, and compliance in Terraform deployments while reducing human intervention and errors.

---

## Step 5: Run GitHub Actions Workflows

### 1️⃣ Trigger Workflow Manually

To trigger the workflow:

1. Navigate to **Actions** in your GitHub repository.
2. Select the workflow you want to run (**Terraform Plan** or **Terraform Apply**).
3. Click **Run workflow** to start the pipeline.

### 2️⃣ Monitor Execution

- View real-time logs under **Actions**.
- Approve Terraform Apply when prompted.

**Impact:** Running the workflows automates infrastructure deployment, improves security, and enforces best practices.

---

## Step 6: Verify Terraform Deployment

After the GitHub Actions workflow completes:

- Check the Terraform Cloud UI (if used) for applied infrastructure.
- Verify deployed AWS resources in the AWS Management Console.

**Impact:** Verifying deployment ensures that infrastructure changes align with the intended configuration.

---

## Step 7: Cleanup Resources (Optional)

To avoid unnecessary costs:

- Manually trigger the **Terraform Destroy** workflow from GitHub Actions.
- Alternatively, run the following command locally:

```sh
terraform destroy -auto-approve
```

**Impact:** Cleaning up resources prevents incurring charges for unused infrastructure and maintains a clean environment.

---

## Summary of Objectives Completed

This repository successfully integrates:

- **Infrastructure as Code (IaC)** with Terraform.
- **CI/CD automation** using multiple GitHub Actions workflows.
- **AWS infrastructure provisioning** with Terraform.
- **Automated Terraform planning and deployment**.
- **Secure authentication** using GitHub Secrets.

By following these steps, you ensure a **scalable, automated, and secure infrastructure deployment process**. For contributions or issues, submit a **Pull Request** or open an **Issue** in GitHub!

**Happy Automating!** 🚀
