# 🧩 What is Jenkins?

Jenkins is an open-source automation server used to automate the building, testing, and deployment of software. It supports Continuous Integration (CI) and Continuous Delivery/Deployment (CD) pipelines.

---

## 🧱 Jenkins Basics

✅ **Features:**
- Open-source and extensible with plugins
- Web-based UI
- Supports distributed builds
- Integrates with Git, Docker, Maven, etc.
- Supports pipelines (scripted or declarative)

---

## 📦 Installation

- **Windows/Linux/Mac:** Install via .war file, package managers, or containers.
- Jenkins runs on port **8080** by default.

---

## 🔗 Jenkins Architecture

1. **Jenkins Agents** – Executes jobs assigned by master.
2. **Jenkins Master** – Controls the build schedule.
3. **Executor** – A slot where the job runs on an agent.

---

## 🔧 Jenkins Job Types

- **Freestyle Project** – Basic job with simple steps.
- **Pipeline** – Code-defined CI/CD process using Jenkinsfile.
- **Multibranch Pipeline** – Auto-detect branches and run jobs.
- **Folder** – Organize multiple jobs.
- **Maven/Gradle Project** – For Java build tools.

---

## 🔌 Jenkins Plugins (Must-Know for DevOps)

- Git Plugin
- Docker Pipeline
- Blue Ocean
- Credentials Binding
- Pipeline: GitHub
- Slack Notification
- Ansible
- Kubernetes CI/CD

---

## 🧪 Jenkins Best Practices

- Store Jenkins file in source control.
- Use pipeline over freestyle jobs.
- Secure with role-based access.
- Clean workspace after builds.
- Monitor job health and trends.

---

## Interview Questions

[https://github.com/I-am-nk/Jenkins-Zero-To-Hero/blob/main/Interview_Questions.md](https://github.com/I-am-nk/Jenkins-Zero-To-Hero/blob/main/Interview_Questions.md)

---

## 🔰 Basic Jenkins Interview Questions and Answers

**1. What is Jenkins?**  
Jenkins is an open-source automation server used for continuous integration and continuous delivery (CI/CD). It helps automate the process of building, testing, and deploying applications.

**2. Why do we use Jenkins in DevOps?**  
Jenkins enables automation in the DevOps lifecycle. It continuously integrates code changes, runs tests, and deploys applications — reducing manual effort, minimizing errors, and improving delivery speed.

**3. How does Jenkins support CI/CD?**
- **CI (Continuous Integration):** Jenkins pulls code from version control (e.g., Git), builds it, and runs tests.
- **CD (Continuous Delivery):** Jenkins can deploy the code to staging/production environments automatically.

**4. How do you install Jenkins?**
Jenkins can be installed on:
- Windows/Linux/Mac by downloading from the official website
- Docker:

```
docker run -p 8080:8080 jenkins/jenkins:lts

```

- Cloud platforms like AWS EC2

**5. What are the types of jobs in Jenkins?**
- Freestyle Project: Basic job configuration
- Pipeline: Scripted CI/CD workflows (with Jenkinsfile)
- Multibranch Pipeline: Automatically creates jobs for branches
- Folder: Organize jobs logically

**6. What are some commonly used plugins in Jenkins?**
- Git Plugin – for SCM integration
- Pipeline Plugin – for Jenkinsfiles
- Docker Plugin – to build/run Docker containers
- Blue Ocean – modern UI for pipelines
- Credentials Binding Plugin – for secrets management

**7. How can you trigger a Jenkins job automatically?**
- Webhook from GitHub/GitLab
- SCM polling (check repo for changes periodically)
- Cron schedules (e.g., H/15 * * * *)
- Downstream jobs from other pipelines

**8. What is a Jenkins Pipeline?**  
A Jenkins Pipeline is a set of instructions written in a Jenkinsfile that defines how software should be built, tested, and deployed. It supports complex workflows and automation.

**9. What’s the difference between Freestyle and Pipeline jobs?**
- **Freestyle:** UI-based, simple to set up but limited
- **Pipeline:** Code-based, more powerful and flexible (supports versioning, complex stages, etc.)

**10. Where is Jenkins installed by default?**
- Linux: `/var/lib/jenkins`
- Windows: `C:\Program Files (x86)\Jenkins` (or the custom path you choose)
- Jenkins Home can be checked using the `$JENKINS_HOME` environment variable.
