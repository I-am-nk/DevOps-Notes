# 🌩️ What Is “Terraform Drift”?

Terraform drift happens when the actual state of your cloud resources (in AWS, Azure, etc.) no longer matches your Terraform configuration.

✅ **Example**:  
You created an EC2 instance via Terraform, but later —
- someone manually changed the instance type in the AWS console, or
- deleted a resource manually, or
- added a tag outside of Terraform.

Terraform’s state file still thinks everything matches the .tf code, but in reality — it doesn’t. That’s configuration drift.

---

## 🧠 Why It Matters

- It breaks infrastructure consistency and reproducibility.
- Can cause unexpected destroys or overwrites when you run `terraform apply`.
- Drift detection helps you identify such manual or external changes before they cause damage.

---

## 🔍 How to Detect Drift in Terraform

### 🧩 Command:

```
terraform plan
```

### 💡 Explanation:
When you run:

```
terraform plan
```

Terraform:
1. Reads your current Terraform configuration (.tf files)
2. Reads the current Terraform state (terraform.tfstate)
3. Queries the real infrastructure from your provider (like AWS)
4. Compares the actual infrastructure to the state file  
   → If anything changed manually, Terraform will show a difference (drift)

So effectively:
`terraform plan` = Detect drift + Show what Terraform would change to fix it.

---

### 🔍 Example Output

```
$ terraform plan

~ aws_instance.my_ec2
instance_type: "t2.micro" => "t3.micro"

```

👀 This means someone manually changed the EC2 instance type in AWS.  
Terraform detected this drift and is showing that it would update it back to match the .tf file (`t2.micro`).

---

### 🧩 Optional: Use terraform apply -refresh-only

If you only want to update your state file to reflect what’s currently deployed (without making changes), use:

```
terraform apply -refresh-only

```
✅ This refreshes the Terraform state with real-world data — helpful when you just want to detect and record the drift, not fix it yet.

---

### 🧩 Another Option: Terraform Cloud / Terraform Enterprise

If you use Terraform Cloud or Enterprise, it has a “Drift Detection” feature built in:
- It automatically detects changes made outside Terraform.
- It can send alerts or trigger runs when drift is found.

**Note**:  
Command-line Terraform doesn’t auto-detect drift — you detect it only by running `terraform plan` or `terraform refresh`.

---

## 🧠 Bonus Tip: Automation for Drift Detection

You can automate drift detection using CI/CD tools:  
Example GitHub Action or Jenkins job:

```
terraform init
terraform plan -detailed-exitcode

```


The `-detailed-exitcode` flag helps automate drift detection:

| Exit Code | Meaning                       |
|-----------|------------------------------|
| 0         | No changes (no drift)         |
| 1         | Error occurred                |
| 2         | Drift detected (changes present) |

So, in automation pipelines:
terraform plan -detailed-exitcode || echo "Drift Detected!"


---

## ✅ Summary

| Action                     | Command                          | Purpose                                         |
|----------------------------|----------------------------------|-------------------------------------------------|
| Detect drift manually      | terraform plan                   | Compares config ↔ state ↔ real infra             |
| Update state only          | terraform apply -refresh-only    | Syncs state file with real infra                 |
| Detect drift in pipelines  | terraform plan -detailed-exitcode| Use exit code to trigger alerts                  |
| Auto-detect drift (Cloud)  | Terraform Cloud “Drift Detection”| Managed & automated detection                    |


