# Infrastructure as Code (IaC) & Terraform – Complete Notes

---

# 🏗️ What is Infrastructure as Code (IaC)?
**Ans:-** Infrastructure as Code (IaC) is the practice of managing and provisioning computing infrastructure (like servers, networks, databases) using code instead of manually setting it up through a UI or CLI.

## 💡 Why IaC is Important:
- 🔄 Consistency – Same environment across dev, staging, production
- ⏱️ Faster Deployments – You can spin up 100 servers with one command
- 📜 Version Control – Changes are tracked in Git like any other code
- 🧪 Testability – You can test infrastructure the same way you test app code
- 📦 Reusability – Share and reuse modules across projects

---

# What is Terraform?
**Ans:-** Terraform is an open-source IaC tool created by HashiCorp that allows you to define and provision infrastructure using a declarative language called HCL (HashiCorp Configuration Language).

## 🔄 Why Use Terraform:
- 🌐 Supports multiple cloud providers (AWS, Azure, GCP, etc.)
- 📦 Reusable modules (like functions for infra)
- 💾 Keeps track of infrastructure state (via .tfstate files)
- ✅ Plan + Apply workflow (review before executing)
- 🌐 It automate the changes and it's also collaborative.

---

## 📌 Terraform Key Concepts to Know:

| Concept   | Meaning                                         |
|-----------|-------------------------------------------------|
| Provider  | Cloud platform (e.g., AWS, Azure, GCP)          |
| Resource  | Infrastructure component (e.g., EC2, VPC)       |
| Module    | A reusable set of resources                     |
| State     | Tracks current infrastructure                   |
| Variable  | Dynamic input (like parameters in code)         |

---

## 🔄 Terraform Lifecycle

Write --> Initialize --> Plan --> Apply --> Destroy

---

## 🔄 Terraform Lifecycle Stages
Terraform's lifecycle includes 5 core stages, which define how Terraform manages infrastructure from start to finish:

### 1. Write (Configuration Phase)
You write `.tf` files using HCL (HashiCorp Configuration Language) to describe the desired infrastructure:
- Define providers (like AWS, Azure)
- Define resources (like EC2 instances, S3 buckets)
- Optionally define variables and outputs
#### 📄 Example:

resource "aws_instance" "example" {
ami = "ami-123456"
instance_type = "t2.micro"
}


---

### 2. Initialize (`terraform init`)
- Downloads the required provider plugins
- Initializes the working directory
- Sets up the `.terraform` directory
- ✅ One-time step per project or whenever provider/plugins change

---

### 3. Plan (`terraform plan`)
- Terraform compares your code to the real-world infrastructure (using the state file)
- Outputs an execution plan showing what changes will happen (create, update, destroy)
- ✅ Safe way to review changes before applying them

---

### 4. Apply (`terraform apply`)
- Applies the planned changes to the real infrastructure
- Creates/updates/destroys resources
- Updates the terraform `.tfstate` file with the new state
- 🔒 This state file helps Terraform track what it has created and manage updates

---

### 5. Destroy (`terraform destroy`) *(Optional but powerful)*
- Destroys all infrastructure defined in your `.tf` files
- Useful for tearing down test environments or cleaning up after a project
- ⚠️ Dangerous if misused, especially in production

---

## Modules:
It is a reusable piece of Terraform code. You call them in your main code to avoid copy-paste, ensure standardization, and keep big infrastructure manageable and DRY (Don’t Repeat Yourself).

### How Modules Work
**1. Create a Module (Reusable Code Block)**
Suppose you want to make a reusable VPC. You’d create a folder `network/` with files like:

```
network/
├── main.tf
├── variables.tf
└── outputs.tf
```


Inside, you’d write normal Terraform resources and logic, plus variables for input.

---

**2. Call the Module from Your Main Code**
In your main Terraform code, you use the `module` block:

```
module "network" {
source = "./network"
vpc_name = "myapp-vpc"
subnet_count = 3
}
```

`source` tells Terraform where to find the module folder (it can also be a Git repo or Terraform Registry URL).
Pass in values as needed (these map to variable definitions in the module).

---

**3. When You Run Terraform**
- Terraform copies the module’s code into your configuration, using the values you provided.
- All resources defined in the module are managed as if you’d declared them directly in your main code.
- You can use the same module multiple times, with different parameters for different environments or projects.

---

**4. Outputs**
- Modules can define `output` values to pass information (like IDs or URLs) back to the calling code.

---

### Why Use Modules?
- **Reusability:** Avoid repeating code for similar infrastructure.
- **Consistency:** Ensures every deployment uses the same logic and best practices.
- **Organization:** Keeps codebase tidy and manageable.
- **Teamwork:** Modules can be stored in registries or VCS and shared across teams.

---

## 🧠 Bonus: Terraform Lifecycle in Interviews
If you're asked in an interview:  
*"Can you explain the Terraform lifecycle?"*
> Terraform follows a lifecycle starting with writing HCL configuration files, initializing the working directory with terraform init, reviewing the execution plan using terraform plan, applying changes with terraform apply, and optionally tearing everything down with terraform destroy. The .tfstate file helps Terraform keep track of the real state of infrastructure, ensuring future changes are applied accurately.

---

## Problems with Terraform
- State file is single source of truth.
- Manual changes to the cloud provider cannot be identified and auto-corrected.
- Not a GitOps friendly tool. Doesn't play well with Flux or Argo CD.
- Can become very complex and difficult to manage.
- Trying to position as a configuration management tool as well.

---

# Interview Questions of Terraform

1. **What is Terraform?**  
   Definition: Terraform is an Infrastructure as Code (IaC) tool that allows users to define and provision data center infrastructure using a declarative configuration language.

2. **What are the key benefits of using Terraform?**  
   Ans:- Infrastructure as Code: Enables version control and collaboration. Multi-Cloud Support: Manage resources across different cloud providers. Execution Plans: Preview changes before applying them. Resource Graph: Understand dependencies and parallelize resource creation.

3. **What is a Terraform Provider?**  
   Definition: A provider is a plugin that allows Terraform to interact with cloud providers, SaaS providers, and other APIs.

4. **Describe the Terraform lifecycle.**  
   Write: Create configuration files. Init: Initialize the working directory. Plan: Create an execution plan. Apply: Execute the changes. Destroy: Remove all resources defined in the configuration.

5. **What is a Terraform State File?**  
   Definition: The state file tracks the resources managed by Terraform and their current state, crucial for mapping real-world resources to your configuration.

6. **How do you manage sensitive data in Terraform?**  
   Methods: Use Terraform variables with sensitive attributes or environment variables to avoid hardcoding sensitive information in configuration files.

7. **What is the purpose of the terraform plan command?**  
   Function: It shows what actions Terraform will take to change the infrastructure to match the configuration files without making any actual changes.

8. **What are Terraform Modules?**  
   Definition: Modules are containers for multiple resources that are used together, allowing for reusability and organization of Terraform code.

9. **How do you implement remote state management in Terraform?**  
   Approach: Use remote backends like Amazon S3 for storing state files and DynamoDB for state locking to prevent concurrent modifications.

10. **What are some common challenges you have faced while using Terraform?**  
    Challenges: Issues with state file corruption, manual changes to cloud resources that Terraform cannot detect, and managing dependencies between resources.

11. **Can you explain the difference between local and remote state?**  
    Local State: Stored on the local machine, not suitable for team collaboration.  
    Remote State: Stored in a remote backend (e.g., S3), allowing multiple users to collaborate and preventing state file conflicts.

12. **What is the significance of the terraform apply command?**  
    Function: It applies the changes required to reach the desired state of the configuration, creating, updating, or destroying resources as necessary.

13. **How do you handle versioning in Terraform?**  
    Method: Use the required_version block in the configuration to specify which version of Terraform is required.

14. **What is the purpose of the terraform output command?**  
    Function: It displays the output values defined in the configuration, useful for accessing information about created resources.

15. **How do you troubleshoot Terraform errors?**  
    Approach: Check the error messages, use terraform plan to see what changes are being proposed, and refer to the Terraform documentation for guidance on specific issues.
