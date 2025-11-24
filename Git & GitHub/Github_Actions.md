# 🧠 What is GitHub Actions?
GitHub Actions is a CI/CD and automation tool built directly into GitHub. It allows you to automate tasks like building code, running tests, deploying applications, and more — all triggered by events like pushing code or opening a pull request.

---

## 💼 Why DevOps Engineers Use GitHub Actions

### 🔧 Common Daily Uses

| Task                          | Description                                            |
|-------------------------------|--------------------------------------------------------|
| CI (Continuous Integration)    | Automatically test code when pushed to a repo.         |
| CD (Continuous Deployment/Delivery) | Automatically deploy apps to servers or cloud.   |
| Code Formatting               | Auto-check for code style or issues before merging.    |
| Docker Image Builds           | Build and push Docker images to Docker Hub or ECR.     |
| Security Scanning             | Run vulnerability scans (e.g., Trivy, Snyk).           |
| Infrastructure Deployment     | Run Terraform, Ansible, or CloudFormation for IaC.     |
| Slack/Teams Notifications     | Send messages after successful or failed builds.        |

---

## 🔁 GitHub Actions Flow (How It Works)

1. Developer pushes code to GitHub  
   ↓  
2. GitHub triggers an Action based on a workflow file  
   ↓  
3. The workflow defines jobs (build, test, deploy)  
   ↓  
4. Each job runs in a GitHub-hosted runner (Ubuntu/Windows/macOS)  
   ↓  
5. Results are shown in GitHub UI (Success/Fail/Logs)

---

## 📂 What is a Workflow?

A workflow is a YAML file stored in `.github/workflows/` folder in your GitHub repo.  
It contains instructions for what to do and when to do it.

---

### ✍️ Example: Simple Workflow File

**Path:**  
`.github/workflows/ci.yml`

```

name: CI Pipeline
on:
push:
branches:
- main
jobs:
build:
runs-on: ubuntu-latest
steps:
- name: Checkout code
uses: actions/checkout@v3
- name: Set up Node.js
uses: actions/setup-node@v3
with:
node-version: '18'
- name: Install dependencies
run: npm install
- name: Run tests
run: npm test

```


**This pipeline:**  
- Triggers on push to main  
- Checks out the repo  
- Sets up Node.js  
- Installs dependencies  
- Runs tests

---

## 🔐 Secrets in GitHub Actions

- Go to GitHub repo → Settings → Secrets and variables → Actions
- Add things like AWS_ACCESS_KEY_ID, DOCKER_PASSWORD

**In your workflow, use them like:**


```
env:
AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```


---

## ⚙️ Benefits of GitHub Actions for DevOps

| Feature                  | Benefit                       |
|--------------------------|-------------------------------|
| Native GitHub integration| No need for external CI tools |
| YAML-based               | Easy to write & version       |
| Fast runners             | GitHub-hosted VMs to run jobs |
| Marketplace              | Thousands of prebuilt actions |
| Secure secrets management| Easy environment variable injection |

---

## Comparing with Jenkins

### Advantages of GitHub Actions over Jenkins

- **Hosting:** Jenkins is self-hosted, meaning it requires its own server to run, while GitHub Actions is hosted by GitHub and runs directly in your GitHub repository.
- **User interface:** Jenkins has a complex and sophisticated user interface, while GitHub Actions has a more streamlined and user-friendly interface that is better suited for simple to moderate automation tasks.
- **Cost:** Jenkins can be expensive to run and maintain, especially for organizations with large and complex automation needs. GitHub Actions, on the other hand, is free for open-source projects and has a tiered pricing model for private repositories, making it more accessible to smaller organizations and individual developers.

---

### Advantages of Jenkins over GitHub Actions

- **Integration:** Jenkins can integrate with a wide range of tools and services, but GitHub Actions is tightly integrated with the GitHub platform, making it easier to automate tasks related to your GitHub workflow.

*In conclusion, Jenkins is better suited for complex and large-scale automation tasks, while GitHub Actions is a more cost-effective and user-friendly solution for simple to moderate automation needs.*

---

## ✅ What is a Self-Hosted Runner in GitHub Actions?

A self-hosted runner is a machine (virtual or physical) that you manage and register with GitHub to run GitHub Actions workflows. Instead of using GitHub's cloud-hosted runners, your jobs run on your own infrastructure (like a VM, local server, or EC2 instance).

*If your project is not open source and your code contains sensitive information, it's better to run the GitHub Action workflow on a self-hosted runner.*

---

### 🏗️ How It Works (High-Level)

1. You create a GitHub Actions runner on your server (EC2).
2. That runner connects to GitHub and waits for a job (Runs the commands on EC2 provided by GitHub).
3. When a workflow is triggered (via push or PR), GitHub assigns it to the runner.
4. The job executes on your system.

---

### 🪜 Steps to Setup Self-Hosted Runner (for a repo)

1. Go to your GitHub repo.
2. Click Settings > Actions > Runners > New self-hosted runner.
3. Select OS, download & extract the package.
4. Or follow the steps one by one shown on that page.

---

## 🧠 Summary

- Use GitHub-hosted runners for simplicity, speed, and zero maintenance.
- Use self-hosted runners when you need control, performance, network access, or custom environments.
- If your project is not open source and your code contains sensitive information, it's better to run the GitHub Action workflow on a self-hosted runner.
