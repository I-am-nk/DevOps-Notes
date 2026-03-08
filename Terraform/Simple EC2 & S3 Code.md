# Terraform: EC2 Instance & S3 Bucket — Full Guide

---

## 🗂️ Project Structure
```
terraform-practice/
├── main.tf
├── variables.tf
├── outputs.tf
└── provider.tf
```

---

## 📄 `provider.tf`
```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"   # Official AWS provider from HashiCorp registry
      version = "~> 5.0"          # Use any version >= 5.0 but < 6.0
    }
  }
  required_version = ">= 1.3.0"  # Minimum Terraform CLI version required
}

provider "aws" {
  region = var.aws_region          # AWS region pulled from variables.tf
}
```

**Line-by-line:**
- `terraform {}` → Declares Terraform settings block
- `required_providers` → Tells Terraform which providers to download
- `source = "hashicorp/aws"` → Points to the official AWS plugin on registry.terraform.io
- `version = "~> 5.0"` → Pessimistic constraint: allows patch/minor updates but locks major version
- `required_version` → Prevents running with an incompatible Terraform CLI
- `provider "aws"` → Configures the AWS provider with your region

---

## 📄 `variables.tf`
```hcl
variable "aws_region" {
  description = "AWS region to deploy resources"  # Human-readable doc
  type        = string                             # Must be a string
  default     = "us-east-1"                       # Used if no value is passed
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"                        # Free-tier eligible instance
}

variable "ami_id" {
  description = "Amazon Machine Image ID"
  type        = string
  default     = "ami-0c02fb55956c7d316"           # Amazon Linux 2 in us-east-1
}

variable "bucket_name" {
  description = "Name of the S3 bucket (must be globally unique)"
  type        = string
  default     = "my-practice-bucket-20240101"     # S3 names are globally unique!
}

variable "environment" {
  description = "Environment tag (dev/staging/prod)"
  type        = string
  default     = "dev"
}
```

**Line-by-line:**
- `variable "name" {}` → Declares an input variable you can reuse across files
- `description` → Documentation for the variable (shows in `terraform plan`)
- `type` → Enforces the data type (`string`, `number`, `bool`, `list`, `map`)
- `default` → Optional fallback value; if omitted, Terraform will prompt you

---

## 📄 `main.tf` — EC2 Instance

```hcl
# ─────────────────────────────────────────────
# KEY PAIR (to SSH into EC2)
# ─────────────────────────────────────────────
resource "aws_key_pair" "my_key" {
  key_name   = "my-ec2-key"                      # Name shown in AWS Console
  public_key = file("~/.ssh/id_rsa.pub")         # Reads your local public key file
}

# ─────────────────────────────────────────────
# SECURITY GROUP (firewall rules)
# ─────────────────────────────────────────────
resource "aws_security_group" "ec2_sg" {
  name        = "ec2-security-group"
  description = "Allow SSH and HTTP traffic"

  ingress {
    description = "Allow SSH"
    from_port   = 22                             # Port range start
    to_port     = 22                             # Port range end
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]                  # Allow from ALL IPs (restrict in prod!)
  }

  ingress {
    description = "Allow HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0                              # 0 means all ports
    to_port     = 0
    protocol    = "-1"                           # -1 means all protocols
    cidr_blocks = ["0.0.0.0/0"]                  # Allow all outbound traffic
  }

  tags = {
    Name        = "ec2-sg"
    Environment = var.environment
  }
}

# ─────────────────────────────────────────────
# EC2 INSTANCE
# ─────────────────────────────────────────────
resource "aws_instance" "my_ec2" {
  ami                    = var.ami_id             # Which OS image to use
  instance_type          = var.instance_type      # Hardware size (t2.micro = 1vCPU, 1GB RAM)
  key_name               = aws_key_pair.my_key.key_name  # Reference the key pair above
  vpc_security_group_ids = [aws_security_group.ec2_sg.id] # Attach security group

  root_block_device {
    volume_size = 20                              # 20 GB root disk
    volume_type = "gp3"                           # General Purpose SSD v3
    encrypted   = true                            # Encrypt the disk at rest
  }

  user_data = <<-EOF
    #!/bin/bash
    yum update -y                                 # Update all packages
    yum install -y httpd                          # Install Apache web server
    systemctl start httpd                         # Start Apache
    systemctl enable httpd                        # Auto-start on reboot
    echo "<h1>Hello from Terraform EC2!</h1>" > /var/www/html/index.html
  EOF
  # user_data runs this shell script on first boot (like cloud-init)

  tags = {
    Name        = "my-terraform-ec2"
    Environment = var.environment
  }
}
```

**Key concepts explained:**

| Keyword | What it does |
|---|---|
| `resource` | Declares an infrastructure object to create |
| `aws_instance` | Resource TYPE (tells Terraform it's an EC2) |
| `"my_ec2"` | Local NAME to reference this resource in other places |
| `ami` | The OS image (like an ISO file for a VM) |
| `ingress / egress` | Inbound / Outbound firewall rules |
| `user_data` | Startup script that runs when EC2 first boots |
| `<<-EOF ... EOF` | Heredoc syntax for multiline strings |
| `var.xxx` | References a variable from `variables.tf` |
| `aws_security_group.ec2_sg.id` | Cross-resource reference: `TYPE.NAME.ATTRIBUTE` |

---

## 📄 `main.tf` — S3 Bucket

```hcl
# ─────────────────────────────────────────────
# S3 BUCKET
# ─────────────────────────────────────────────
resource "aws_s3_bucket" "my_bucket" {
  bucket        = var.bucket_name                # Globally unique bucket name
  force_destroy = true                           # Allows `terraform destroy` even if bucket has objects

  tags = {
    Name        = "my-practice-bucket"
    Environment = var.environment
  }
}

# ─────────────────────────────────────────────
# BLOCK ALL PUBLIC ACCESS (security best practice)
# ─────────────────────────────────────────────
resource "aws_s3_bucket_public_access_block" "block_public" {
  bucket = aws_s3_bucket.my_bucket.id            # Link to bucket above

  block_public_acls       = true                 # Block new public ACLs
  block_public_policy     = true                 # Block new public bucket policies
  ignore_public_acls      = true                 # Ignore existing public ACLs
  restrict_public_buckets = true                 # Make bucket fully private
}

# ─────────────────────────────────────────────
# ENABLE VERSIONING (keeps history of objects)
# ─────────────────────────────────────────────
resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.my_bucket.id

  versioning_configuration {
    status = "Enabled"                           # "Enabled" or "Suspended"
  }
}

# ─────────────────────────────────────────────
# SERVER-SIDE ENCRYPTION (AES-256)
# ─────────────────────────────────────────────
resource "aws_s3_bucket_server_side_encryption_configuration" "encryption" {
  bucket = aws_s3_bucket.my_bucket.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"                   # Encrypt all objects with AES-256
    }
  }
}
```

---

## 📄 `outputs.tf`

```hcl
output "ec2_public_ip" {
  description = "Public IP of the EC2 instance"
  value       = aws_instance.my_ec2.public_ip    # Fetches the assigned public IP
}

output "ec2_public_dns" {
  description = "Public DNS of the EC2 instance"
  value       = aws_instance.my_ec2.public_dns
}

output "s3_bucket_name" {
  description = "Name of the created S3 bucket"
  value       = aws_s3_bucket.my_bucket.id
}

output "s3_bucket_arn" {
  description = "ARN of the S3 bucket"
  value       = aws_s3_bucket.my_bucket.arn      # Amazon Resource Name
}
```

**Why outputs matter in interviews:**
- Outputs print values after `terraform apply` runs
- Used by other Terraform modules to consume resource attributes
- Think of them like "return values" of a Terraform configuration

---

## 🚀 Commands to Run (in order)

```bash
terraform init      # Downloads providers & initializes backend
terraform fmt       # Auto-formats your .tf files
terraform validate  # Checks syntax without hitting AWS
terraform plan      # Shows what WILL be created (dry run)
terraform apply     # Actually creates resources on AWS
terraform destroy   # Tears down everything (careful!)
```

---

## 🎯 Interview Cheat Sheet

| Question | Answer |
|---|---|
| What is `terraform init`? | Downloads provider plugins and sets up backend |
| Difference between `plan` and `apply`? | Plan = dry run, Apply = actually provisions |
| What is a state file? | `terraform.tfstate` — tracks real-world resource state |
| What is `depends_on`? | Explicit dependency when Terraform can't auto-detect it |
| What is a remote backend? | Storing state in S3 + DynamoDB instead of locally |
| What is `data` block? | Reads existing AWS resources (doesn't create them) |
| What is `locals`? | Local computed variables within a module |
| What is `count` vs `for_each`? | count = number of copies, for_each = map-based iteration |
