# Ansible Interview Essentials

## 1. What is Ansible?

Ansible is an **open-source automation tool** used for:
- Configuration management
- Application deployment
- Provisioning
- Orchestration
- Infrastructure as Code (IaC)

It uses **YAML** to define automation tasks in "playbooks" and operates over **SSH** (no agents required).

---

## 2. Why Use Ansible?

| Feature      | Benefit                                                                      |
|--------------|------------------------------------------------------------------------------|
| Agentless    | No need to install any software on remote machines (uses SSH)                |
| Simple Syntax| Uses easy-to-read YAML files                                                 |
| Idempotent   | Running a task multiple times gives the same result, ensuring stability      |
| Scalable     | Can manage hundreds or thousands of machines from one control node           |
| Declarative  | You define what you want, not how to do it (e.g., “install nginx”)           |
| Cross-platform| Works with Linux, macOS, Windows, and cloud providers like AWS, Azure, GCP  |

---

## 3. Difference Between Puppet and Ansible

| Feature/Aspect      | Ansible                             | Puppet                                             |
|---------------------|-------------------------------------|----------------------------------------------------|
| Type                | Configuration Management & Orchestration | Primarily Configuration Management                 |
| Language            | YAML (Playbooks)                    | Puppet DSL (Ruby-like Domain Specific Language)     |
| Architecture        | Agentless (uses SSH)                | Agent-based (Puppet agent + Puppet master)         |
| Learning Curve      | Easy (human-readable YAML)          | Steeper (DSL syntax)                               |
| Communication       | Push-based (from control machine)   | Pull-based (agents pull configs from master)        |
| Installation        | Lightweight (just needs SSH)        | Requires installation on client/agent machines      |
| Platform Support    | Cross-platform (Linux, Windows, macOS)| Cross-platform                                 |
| Security            | Uses SSH keys                       | Uses SSL certificates                               |
| Idempotency         | Yes                                 | Yes                                                |
| Integration         | Easy with cloud providers and CI/CD tools | Strong integrations, especially with legacy systems|
| Community & Support | Large open-source community, RedHat supported | Large, mature community, now owned by Perforce (formerly by Puppet Inc.) |

---

## 4. Disadvantages of Ansible

While Ansible is a powerful and agentless automation tool, it does have a few limitations:
- Not ideal for large-scale environments (push-based and can slow down with many nodes).
- Lacks a built-in GUI unless you use Ansible Tower (paid solution).
- Does not have native rollback or state management, so you must build those mechanisms manually.

---

## 5. Which Language Does Ansible Use for Modeling?

"Ansible itself is written in **Python**, and most of its modules are also Python-based. As a user, you write playbooks in **YAML**, which is a simple, declarative language. But under the hood, it's Python doing all the heavy lifting."

---

## 6. Does Ansible Support Linux and Windows?

"Yes, Ansible supports both Linux and Windows systems.
- For **Linux**, it uses SSH to connect, which works out of the box.
- For **Windows**, it connects through WinRM, but requires extra configuration."

---

## 7. Ansible Push or Pull Mechanism

Ansible uses a **push-based mechanism**.

The control node pushes tasks to the managed nodes over SSH (or WinRM for Windows).
It doesn’t require any agent on the target machine, making it lightweight and easy to set up.

---

## 8. What Programming Language Does Ansible Use to Write Playbooks?

"Ansible playbooks are written in **YAML**, a simple, human-readable format.
YAML is used to define tasks, variables, roles, and configurations in a structured way.
It makes Ansible playbooks easy to read, write, and maintain—even for people who aren’t developers."

---

## 9. Does Ansible Support All Cloud Providers?

Yes, Ansible supports all major cloud providers like AWS, Azure, and GCP.

But actually, it doesn’t matter which cloud provider you use—Ansible just needs the **public IP and SSH access** to the server.
As long as it can connect via SSH (or WinRM for Windows), it can manage the machine, regardless of where it's hosted.

---

## 10. Difference Between Ansible Ad Hoc Commands vs Ansible Playbook

### Ansible Ad Hoc Commands
- Quick one-liners for executing simple tasks on the fly.
- No need to create a file—run directly from the command line.
- Ideal for one-time tasks, like:
    - Installing a package
    - Rebooting a server
    - Checking disk space

### Ansible Playbooks
- YAML files that define a set of tasks to run in a structured way.
- Used for **complex automation** like multi-step deployments, configurations, and orchestration.
- Playbooks are **versionable** and **repeatable**.

---
