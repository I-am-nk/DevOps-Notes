# DevOps and SDLC Overview

## What is DevOps?

DevOps is the process of improving application delivery by ensuring proper automation, high code quality, continuous monitoring, and continuous testing. This approach accelerates software delivery and enhances reliability.

### Core Pillars of DevOps (AQMT)

* **Automation**
* **Quality**
* **Continuous Monitoring**
* **Continuous Testing**

## Why DevOps?

DevOps improves collaboration between teams, automates processes, speeds up software delivery, enhances software quality, increases operational efficiency, ensures scalability, and integrates security practices. Overall, it makes software development faster, stable, and more reliable.

---

# SDLC (Software Development Life Cycle)

## What is SDLC?

SDLC is a structured process used for designing, developing, testing, and deploying software applications. It ensures that the software is high‑quality, cost‑effective, and delivered within timelines.

## Phases of SDLC

### 1. Requirement Analysis

* Gather and define project requirements from stakeholders.
* *Example:* A bank wants a mobile app for transactions.

### 2. Planning

* Define scope, timeline, budget, and risks.
* *Example:* Choose tech stack such as Java, React, MySQL.

### 3. Design

* Create system architecture, UI/UX, and models.
* *Example:* Wireframes, database schema.

### 4. Development (Coding)

* Implement the application based on design specifications.
* *Example:* Build login, dashboard, transaction features.

### 5. Testing

* Identify and fix defects via unit, integration, and user testing.
* *Example:* Validate that transactions process correctly.

### 6. Deployment

* Release the application to users (on‑premises or cloud).
* *Example:* Deploy app to Google Play or App Store.

### 7. Maintenance & Monitoring

* Fix bugs, release updates, enhance features.
* *Example:* Security patches, new feature releases.

---

# Agile Methodology

Agile is a flexible, iterative software development and project management methodology. Work is divided into small units called **sprints**, typically 1–2 weeks, enabling frequent delivery of working features.

### Story Point Estimation

Most teams use the **Fibonacci sequence** (1, 2, 3, 5, 8, 13, 21) to estimate effort and uncertainty.

## Key Agile Concepts

| Concept           | Description                                                                |
| ----------------- | -------------------------------------------------------------------------- |
| **Sprint**        | A time‑boxed development cycle (1–2 weeks)                                 |
| **Scrum**         | A widely‑used Agile framework with roles like Scrum Master & Product Owner |
| **User Story**    | A feature defined from the user's perspective                              |
| **Backlog**       | A prioritized list of tasks and features                                   |
| **Daily Standup** | Short daily sync meeting for updates and blockers                          |
| **Sprint Review** | Demo of completed features at sprint end                                   |
| **Retrospective** | Discussion on improvements for the next sprint                             |

---

# Agile + DevOps

Agile and DevOps complement each other:

* **Agile** accelerates development and feedback cycles.
* **DevOps** ensures automated deployments, testing, and operational reliability.

Together, they enable **Continuous Integration and Continuous Delivery (CI/CD)**, resulting in faster and more predictable releases.




# Virtualization Concepts and Container vs VM Comparison

## Definitions

### 1. Server

A physical or virtual machine that provides services, resources, or applications to clients over a network.

### 2. Virtual Machine (VM)

A software-based emulation of a computer that runs on a physical server. It behaves like an independent system with its own operating system and applications.

### 3. Hypervisor

A software layer that enables virtualization by creating and managing multiple VMs on a single physical server.

---

## How They Are Interconnected

* A **server** (hardware) hosts a **hypervisor**.
* The **hypervisor** creates and manages multiple **virtual machines** on the same server.
* Each **VM** operates independently and can run different operating systems and applications.

---

## Key Benefits of Virtualization

* Maximizes hardware utilization
* Isolates applications for better security
* Simplifies deployment and scaling
* Reduces costs by minimizing the need for multiple physical servers

---

# Containers vs Virtual Machines

| Feature                 | Containers                            | Virtual Machines (VMs)                       |
| ----------------------- | ------------------------------------- | -------------------------------------------- |
| **Architecture**        | Shares the host OS kernel             | Has its own OS, runs over a hypervisor       |
| **Boot Time**           | Seconds                               | Minutes                                      |
| **Size**                | Lightweight (MBs)                     | Heavy (GBs)                                  |
| **Resource Usage**      | Minimal (shares kernel, low overhead) | High (each VM requires CPU, RAM, storage)    |
| **Isolation**           | Process-level isolation (less secure) | Full machine-level isolation (more secure)   |
| **Performance**         | Near-native performance               | Slightly slower due to virtualization layer  |
| **Portability**         | Highly portable across environments   | Less portable (depends on OS/hypervisor)     |
| **Use Case**            | Microservices, CI/CD, DevOps          | Monolithic apps, legacy workloads            |
| **Dependency Handling** | Includes only app dependencies        | Contains dependencies within the VM OS image |
| **Management Tools**    | Docker, Podman, Kubernetes            | VMware, VirtualBox, Hyper-V, KVM             |
