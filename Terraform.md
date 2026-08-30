# TERRAFORM — INTERVIEW NOTES

**Start-to-End • Simple to Learn • Easy to Remember • Interview Ready**

> This Markdown version keeps the complete topic coverage from the uploaded PATHNEX Terraform PDF, while reorganizing it into simpler interview explanations, memory tricks, commands, HCL examples, scenarios, and revision sections. The source covers Terraform from introduction through the hands-on AWS project. fileciteturn3file0L5-L30

---

# 1. What is Terraform?

Terraform is an **open-source Infrastructure as Code (IaC) tool**.

It allows you to:

- Define infrastructure
- Provision infrastructure
- Automate infrastructure management

Terraform uses a high-level configuration language called:

> **HCL — HashiCorp Configuration Language**

Terraform can automate infrastructure such as:

- Servers
- Storage
- Networks
- And other infrastructure components

### Interview Answer

> **Terraform is an open-source Infrastructure as Code tool used to define, provision, and manage infrastructure using declarative configuration written in HCL.**

### Memory Trick

**Terraform = IaC + HCL + AUTOMATE INFRASTRUCTURE**

---

# 2. Why Use Terraform?

The source gives three major reasons.

---

## 2.1 Declarative Syntax

You define:

> **WHAT infrastructure you need**

rather than:

> **HOW to create it step by step**

### Example

Instead of manually explaining every step to create an EC2 instance, you define the desired EC2 resource in Terraform.

### Memory Trick

**Declarative = WHAT, NOT HOW**

---

## 2.2 Infrastructure as Code

Infrastructure configuration can be treated like code.

This allows you to:

- Version-control infrastructure
- Review infrastructure changes
- Reuse configuration

### Interview Answer

> **Terraform allows infrastructure to be managed as code, so the configuration can be version-controlled like application code.**

### Memory Trick

**IaC = INFRASTRUCTURE IN CODE**

---

## 2.3 Platform Agnostic

Terraform supports major platforms such as:

- AWS
- Azure
- Google Cloud
- On-premises infrastructure

### Interview Answer

> **Terraform is platform agnostic and supports major cloud providers as well as on-premises infrastructure.**

### Memory Trick

**Terraform = MULTI-PLATFORM**

---

# 3. Key Terraform Concepts

The source introduces four core concepts:

1. Providers
2. Resources
3. Modules
4. State

---

## 3.1 Providers

Providers are the cloud platforms or services Terraform interacts with.

Examples:

- AWS
- Azure

### Simple Understanding

```text
Terraform
    ↓
Provider
    ↓
Cloud / Service
```

### Interview Answer

> **A provider is the plugin Terraform uses to interact with a particular cloud platform or service, such as AWS or Azure.**

### Memory Trick

**Provider = CONNECTOR**

---

## 3.2 Resources

Resources define the actual infrastructure components.

Examples:

- Virtual machines
- Storage

### Interview Answer

> **A resource represents an infrastructure component that Terraform creates or manages.**

### Memory Trick

**Resource = ACTUAL INFRASTRUCTURE**

---

## 3.3 Modules

Modules are reusable sets of Terraform configuration files.

They help:

- Organize code
- Reuse code

### Interview Answer

> **A module is a reusable collection of Terraform configuration used to organize and standardize infrastructure code.**

### Memory Trick

**Module = REUSE**

---

## 3.4 State

Terraform tracks infrastructure state.

It uses the state to determine:

> **What changes are needed?**

### Interview Answer

> **Terraform state keeps track of the infrastructure Terraform manages and helps Terraform determine the difference between the desired configuration and the tracked infrastructure state.**

### Memory Trick

**State = MEMORY**

---

# 4. HCL vs Bash

The source explicitly emphasizes this distinction.

## HCL

HCL is used for:

- Terraform configuration files
- Defining infrastructure

Example:

```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

## Bash

Bash is used to execute Terraform commands in the terminal.

Example:

```bash
terraform init
terraform plan
terraform apply
```

### Interview Answer

> **HCL is the configuration language I use to define Terraform infrastructure, while Bash is the shell I use to execute Terraform CLI commands.**

### Memory Trick

**HCL = DEFINE**

**BASH = RUN COMMANDS**

---

# 5. Setting Up Terraform

## Step 1 — Install Terraform

Install Terraform according to your operating system.

After installation, verify it using:

```bash
terraform --version
```

### Memory Trick

**Install → Verify**

---

# 6. Configure a Provider

The source uses AWS as the example.

To interact with AWS, configure the AWS provider in Terraform.

AWS credentials are needed.

The source says credentials can be supplied through:

- AWS CLI
- Environment variables

---

## Example `provider.tf`

```hcl
provider "aws" {
  region = "us-west-2"
}
```

### Understand

```text
provider "aws"
       ↓
   AWS Provider
       ↓
region = us-west-2
```

### Interview Answer

> **To use AWS with Terraform, I configure the AWS provider and provide the required AWS credentials through the AWS CLI or environment variables.**

### Memory Trick

**Provider = WHERE Terraform connects**

---

# 7. Writing Terraform Configuration

---

## Step 1 — Define a Resource

Terraform uses resource blocks to define infrastructure components.

The source gives an AWS EC2 example.

### `main.tf`

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

---

# 8. Understand the Resource Block

The source explains:

```hcl
resource "aws_instance" "my_ec2" {
```

### `aws_instance`

This is the:

> **Resource type**

It represents an EC2 instance.

### `my_ec2`

This is the:

> **Resource name**

The name can be chosen by you.

### `ami`

Specifies:

> **AMI to use**

### `instance_type`

Specifies:

> **Instance type**

### Memory Trick

```text
resource "TYPE" "NAME"

TYPE = What?
NAME = Which one?
```

---

# 9. Terraform Initialize

Before applying changes, run:

```bash
terraform init
```

Terraform initialization:

- Initializes the working directory.
- Downloads the necessary provider plugins.

### Interview Answer

> **`terraform init` initializes the Terraform working directory and downloads the required provider plugins.**

### Memory Trick

**INIT = PREPARE TERRAFORM**

---

# 10. Terraform Command Lifecycle

The core flow is:

```text
terraform init
       ↓
terraform plan
       ↓
terraform apply
       ↓
Infrastructure
```

If required:

```text
terraform destroy
```

And before execution:

```text
terraform validate
```

---

# 11. `terraform plan`

Command:

```bash
terraform plan
```

Terraform:

- Reads configuration files.
- Compares them with the current infrastructure state.
- Shows the changes it plans to make.

### Important

`plan` **does not actually make the infrastructure changes**.

### Interview Answer

> **`terraform plan` compares the Terraform configuration with the current state and shows what changes Terraform intends to make.**

### Memory Trick

**PLAN = PREVIEW**

---

# 12. `terraform apply`

Command:

```bash
terraform apply
```

This actually makes the changes to infrastructure.

### Interview Answer

> **`terraform apply` applies the planned configuration and makes the infrastructure changes.**

### Memory Trick

**APPLY = ACT**

---

# 13. `terraform destroy`

Command:

```bash
terraform destroy
```

Used to tear down everything Terraform created.

### Interview Answer

> **`terraform destroy` removes the infrastructure managed by the Terraform configuration.**

### Memory Trick

**DESTROY = DELETE INFRASTRUCTURE**

---

# 14. `terraform validate`

Command:

```bash
terraform validate
```

Validates Terraform configuration files for syntax errors.

### Interview Answer

> **`terraform validate` checks the Terraform configuration for syntax and configuration errors before planning or applying.**

### Memory Trick

**VALIDATE = CHECK CONFIG**

---

# 15. Terraform Variables

Terraform variables make configuration:

- Flexible
- Reusable

---

## Example `variables.tf`

```hcl
variable "instance_type" {
  description = "The instance type"
  default     = "t2.micro"
}
```

### Why Use Variables?

Instead of hard-coding:

```hcl
instance_type = "t2.micro"
```

you can use:

```hcl
instance_type = var.instance_type
```

This makes the configuration reusable.

### Interview Answer

> **Terraform variables allow me to parameterize the configuration so I can reuse the same Terraform code with different values.**

### Memory Trick

**Variable = INPUT**

---

# 16. Using a Variable in a Resource

```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_type
}
```

Here:

```text
var.instance_type
       ↓
Variable value
       ↓
EC2 instance type
```

---

# 17. Terraform Outputs

Outputs allow you to display important information about resources you created.

---

## Example `outputs.tf`

```hcl
output "instance_public_ip" {
  value = aws_instance.my_ec2.public_ip
}
```

This can expose the public IP of the EC2 instance.

### Interview Answer

> **Terraform outputs expose important information from created resources, such as an instance's public IP.**

### Memory Trick

**Output = INFORMATION OUT**

---

# 18. Variables vs Outputs

Easy interview comparison:

| Concept | Purpose |
|---|---|
| Variable | Input to Terraform configuration |
| Output | Information returned/displayed from infrastructure |

### Memory Trick

**Variable = IN**

**Output = OUT**

---

# 19. Terraform State

Terraform maintains a state file:

```text
terraform.tfstate
```

The source says Terraform uses it to:

- Keep track of managed resources.
- Detect changes between actual infrastructure and configuration.

### Interview Answer

> **Terraform state is Terraform's record of the infrastructure it manages. It is used to track resources and determine what changes are required.**

### Memory Trick

**STATE = TERRAFORM'S MEMORY**

---

# 20. Important State Commands

## List resources

```bash
terraform state list
```

Lists all resources in the state file.

---

## Show a resource

```bash
terraform state show <resource>
```

Shows detailed state information for a specific resource.

### Memory Trick

```text
state list
    ↓
WHAT resources?

state show
    ↓
DETAILS of one resource
```

---

# 21. Remote State Storage

For teams, the source recommends storing Terraform state remotely.

Example:

> **S3 bucket**

Why?

- Easier team collaboration
- Avoids conflicts
- Helps ensure consistency

### Interview Answer

> **For team environments, Terraform state can be stored remotely, for example in an S3 bucket, so multiple team members can work with a shared state location.**

### Memory Trick

**Remote State = TEAM SHARED MEMORY**

---

# 22. Terraform Modules

A module is a container for multiple resources used together.

Modules help:

- Organize Terraform code.
- Reuse Terraform code.

### Interview Answer

> **A Terraform module is a reusable container of related Terraform configuration and resources.**

### Memory Trick

**MODULE = PACKAGE OF REUSABLE INFRASTRUCTURE**

---

# 23. Creating a Module

The source gives an EC2 instance module.

## Step 1 — Create folder

```text
modules/ec2-instance/
```

Create:

```text
main.tf
variables.tf
```

---

## Step 2 — Module `main.tf`

```hcl
resource "aws_instance" "my_instance" {
  ami           = var.ami
  instance_type = var.instance_type
}
```

The module receives values through variables.

---

## Step 3 — Module `variables.tf`

```hcl
variable "ami" {
  description = "AMI ID for EC2 instance"
}

variable "instance_type" {
  description = "EC2 instance type"
}
```

---

## Step 4 — Use Module from Root Configuration

```hcl
module "ec2_instance" {
  source        = "./modules/ec2-instance"
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

### Understand

```text
Root Configuration
       ↓
Module
       ↓
Reusable EC2 Configuration
       ↓
EC2 Resource
```

### Interview Answer

> **I can create an EC2 module with variables for AMI and instance type, then call that module from the root configuration using the module source path.**

---

# 24. Remote Backends

Remote backends store the Terraform state remotely.

The source says they make it easier for teams to collaborate.

---

## Example `backend.tf`

```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "state/terraform.tfstate"
    region = "us-west-2"
  }
}
```

### Understand

```text
Terraform
    ↓
Remote Backend
    ↓
S3
    ↓
terraform.tfstate
```

### Interview Answer

> **A remote backend stores Terraform state in a remote location such as S3, making shared Terraform work easier for teams.**

### Memory Trick

**Backend = WHERE STATE LIVES**

---

# 25. Terraform Lifecycle

The source defines the `lifecycle` block as controlling how resources are:

- Created
- Updated
- Destroyed

It is used **inside a resource block**.

---

## Basic Syntax

```hcl
resource "<provider>_<type>" "<name>" {
  # resource config

  lifecycle {
    # lifecycle rules
  }
}
```

### Interview Answer

> **Terraform lifecycle rules control how a resource is created, updated, and destroyed. The lifecycle block is defined inside a resource block.**

### Memory Trick

**Lifecycle = CONTROL RESOURCE BEHAVIOR**

---

# 26. Lifecycle Arguments — C-P-I-R

The source covers four lifecycle arguments:

1. `create_before_destroy`
2. `prevent_destroy`
3. `ignore_changes`
4. `replace_triggered_by`

### Master Memory Trick

> **C-P-I-R**

```text
C → Create before destroy
P → Prevent destroy
I → Ignore changes
R → Replace triggered
```

The source's quick summary table gives the purpose as:
- create_before_destroy → Zero downtime replacement
- prevent_destroy → Protect resource
- ignore_changes → Ignore drift
- replace_triggered_by → Force rebuild fileciteturn3file0L255-L272

---

# 27. `create_before_destroy`

This creates a new resource **before deleting the old one**.

```hcl
lifecycle {
  create_before_destroy = true
}
```

## Use Cases

The source mentions:

- Zero downtime deployments
- Load balancers
- Servers

## Notes

It may:

- Increase cost temporarily.
- Fail if names must be unique.

### Interview Answer

> **`create_before_destroy` creates the replacement resource before destroying the existing one. It can help with zero-downtime replacements, although it may temporarily increase cost or fail when resource names must be unique.**

### Memory Trick

**C = CREATE FIRST**

---

# 28. `prevent_destroy`

Prevents accidental deletion.

```hcl
lifecycle {
  prevent_destroy = true
}
```

## Use Cases

- Production database
- Critical infrastructure

The source says Terraform will throw an error on destroy.

### Interview Answer

> **`prevent_destroy` protects critical resources from accidental deletion. If Terraform attempts to destroy such a protected resource, Terraform throws an error.**

### Memory Trick

**P = PROTECT**

---

# 29. `ignore_changes`

Ignores changes to selected resource attributes.

```hcl
lifecycle {
  ignore_changes = [tags]
}
```

## Use Case

The source mentions external updates such as:

- Autoscaling
- Tags

### Ignore All Changes

```hcl
ignore_changes = all
```

## Risk

The source warns:

> It can hide configuration drift.

### Interview Answer

> **`ignore_changes` tells Terraform to ignore changes to selected attributes. It can be useful when external systems modify those attributes, but overusing it can hide configuration drift.**

### Memory Trick

**I = IGNORE**

---

# 30. `replace_triggered_by`

Forces resource replacement when a dependency changes.

```hcl
lifecycle {
  replace_triggered_by = [aws_ami.latest]
}
```

## Use Case

The source gives:

> Rebuild EC2 when the AMI changes.

It also mentions:

> Immutable infrastructure

### Interview Answer

> **`replace_triggered_by` forces a resource replacement when a specified dependency changes. For example, it can be used to rebuild an EC2 instance when an AMI changes.**

### Memory Trick

**R = REBUILD WHEN TRIGGER CHANGES**

---

# 31. Lifecycle Quick Summary

| Argument | Simple Meaning | Source Purpose |
|---|---|---|
| `create_before_destroy` | Create replacement first | Zero-downtime replacement |
| `prevent_destroy` | Protect resource | Prevent accidental deletion |
| `ignore_changes` | Ignore selected changes | Ignore drift |
| `replace_triggered_by` | Force replacement | Force rebuild |

### C-P-I-R

```text
C → Create before destroy
P → Prevent destroy
I → Ignore changes
R → Replace triggered
```

---

# 32. Lifecycle Important Points

The source explicitly notes:

- Lifecycle works only in a **resource block**.
- It is **not applicable to modules**.
- Overusing `ignore_changes` is risky.
- Provider limitations may apply.

### Interview Answer

> **Lifecycle rules are defined inside resource blocks, not modules. I also use `ignore_changes` carefully because it can hide configuration drift, and provider-specific limitations may apply.**

---

# 33. Immutable Infrastructure

The source includes **immutable infrastructure** in the lifecycle section.

A useful way to remember it in the context of the notes:

> Instead of modifying an existing infrastructure resource in place, replace it with a new version when appropriate.

This connects especially well with:

```text
create_before_destroy
replace_triggered_by
```

### Memory Trick

**Immutable = REPLACE, DON'T MODIFY**

---

# 34. Terraform Best Practices

The source gives three best practices.

---

## 34.1 Keep Secrets Secure

Never hard-code secrets such as AWS credentials in Terraform configuration files.

### Interview Answer

> **I never hard-code secrets such as AWS credentials in Terraform configuration. I use secure credential mechanisms such as the AWS CLI or environment-based credentials as described in the source.**

### Memory Trick

**SECRETS = NEVER HARD-CODE**

---

## 34.2 Version Control

The source says:

> Always version-control Terraform code but not the state files.

### Interview Answer

> **I keep Terraform configuration under version control, while the state is handled separately rather than committed with the Terraform code.**

### Memory Trick

**CODE → VERSION CONTROL**

**STATE → HANDLE SEPARATELY**

---

## 34.3 `terraform fmt`

Use:

```bash
terraform fmt
```

It formats Terraform code consistently.

### Interview Answer

> **I use `terraform fmt` to keep Terraform configuration formatted consistently.**

### Memory Trick

**FMT = FORMAT**

---

# 35. Hands-on Terraform Project

The source's final page proposes a hands-on project.

## Project Goal

Create:

- An S3 bucket
- An EC2 instance

in AWS using Terraform.

### Project Flow

```text
Terraform
    ↓
Configure Provider
    ↓
Define Resources
    ↓
S3 Bucket + EC2
    ↓
terraform plan
    ↓
terraform apply
```

---

## Project Requirements from Source

### 1. Create Infrastructure

Create:

- S3 bucket
- EC2 instance

using Terraform and AWS.

### 2. Configure and Deploy

Practice:

- Configuring the provider
- Writing resource blocks
- Planning changes
- Applying changes

### 3. Use Variables

Use Terraform variables to customize:

- Instance type
- Region

### Interview Answer

> **For a hands-on Terraform project, I can configure the AWS provider, define S3 and EC2 resources, use variables for values such as instance type and region, run plan to review changes, and apply the configuration.**

The source explicitly lists this project and the use of variables for instance types and regions. fileciteturn3file0L282-L291

---

# 36. Complete Terraform Workflow

Remember this sequence:

```text
1. Install Terraform
        ↓
2. Configure Provider
        ↓
3. Write HCL
        ↓
4. Define Resources
        ↓
5. terraform init
        ↓
6. terraform validate
        ↓
7. terraform plan
        ↓
8. terraform apply
        ↓
9. Check Outputs / State
        ↓
10. terraform destroy
```

### Master Memory Trick

> **I-V-P-A**

```text
INIT
VALIDATE
PLAN
APPLY
```

Think:

> **Prepare → Check → Preview → Create**

---

# 37. Terraform File Structure

Based on the source examples:

```text
terraform-project/
│
├── provider.tf
├── main.tf
├── variables.tf
├── outputs.tf
└── backend.tf
```

For a module:

```text
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
│
└── modules/
    └── ec2-instance/
        ├── main.tf
        └── variables.tf
```

---

# 38. Provider vs Resource vs Module vs State

This is one of the most important memory sections.

| Concept | Remember As | Purpose |
|---|---|---|
| Provider | CONNECTOR | Connects Terraform to platform/service |
| Resource | INFRASTRUCTURE | Defines actual infrastructure |
| Module | REUSE | Reusable configuration |
| State | MEMORY | Tracks managed infrastructure |

### One-line trick

> **Provider connects, Resource creates, Module reuses, State remembers.**

---

# 39. Variable vs Output

```text
Variable
   ↓
INPUT

Terraform
   ↓
Infrastructure

Output
   ↓
INFORMATION OUT
```

### Interview line

> **Variables provide inputs to make configuration reusable, while outputs expose useful information from created resources.**

---

# 40. State vs Backend

These are easy to confuse.

## State

```text
terraform.tfstate
```

It tracks the infrastructure Terraform manages.

## Backend

Defines where the state is stored.

Example:

```text
S3
```

### Memory Trick

**STATE = WHAT TERRAFORM REMEMBERS**

**BACKEND = WHERE THAT MEMORY IS STORED**

---

# 41. `plan` vs `apply` vs `destroy`

| Command | Meaning |
|---|---|
| `terraform plan` | Preview changes |
| `terraform apply` | Make changes |
| `terraform destroy` | Remove managed infrastructure |

### Memory Trick

**PLAN → SEE**

**APPLY → DO**

**DESTROY → REMOVE**

---

# 42. Lifecycle Scenario Questions

## Scenario 1 — Need Zero Downtime

Use:

```hcl
create_before_destroy = true
```

**Think:** Create new → remove old.

---

## Scenario 2 — Protect Production DB

Use:

```hcl
prevent_destroy = true
```

**Think:** Don't accidentally delete.

---

## Scenario 3 — External System Changes Tags

Use:

```hcl
ignore_changes = [tags]
```

**Think:** Terraform should ignore selected external changes.

**Warning:** It can hide drift.

---

## Scenario 4 — AMI Changes and EC2 Must Rebuild

Use:

```hcl
replace_triggered_by = [aws_ami.latest]
```

**Think:** Dependency changes → replacement.

---

# 43. Interview Traps to Avoid

## Trap 1 — Declarative vs Imperative

Terraform is described in the source as **declarative**.

Say:

> **I define what infrastructure I want.**

Do not describe the core Terraform model as a step-by-step procedure.

---

## Trap 2 — HCL vs Bash

```text
HCL  → Terraform configuration
Bash → Terraform commands
```

---

## Trap 3 — Plan vs Apply

```text
plan  → Shows intended changes
apply → Actually makes changes
```

---

## Trap 4 — Variable vs Output

```text
Variable → Input
Output   → Information out
```

---

## Trap 5 — State vs Backend

```text
State   → Tracks infrastructure
Backend → Stores state
```

---

## Trap 6 — Module vs Resource

```text
Resource → Infrastructure component
Module   → Reusable group of configuration/resources
```

---

## Trap 7 — `ignore_changes`

Do not say:

> It makes drift disappear.

The source specifically warns:

> It can hide configuration drift.

---

## Trap 8 — Lifecycle Location

The source says lifecycle:

> Works only in a resource block.

It is:

> Not applicable to modules.

---

## Trap 9 — Secrets

Never hard-code AWS credentials in Terraform configuration.

---

# 44. One-Minute Interview Answer — Terraform

If the interviewer asks:

> **“Tell me about Terraform.”**

Use this:

> **Terraform is an open-source Infrastructure as Code tool from HashiCorp that allows us to define and provision infrastructure using declarative HCL configuration. It supports platforms such as AWS, Azure, Google Cloud, and on-premises infrastructure. The main concepts are providers, resources, modules, and state. Providers connect Terraform to platforms, resources define infrastructure, modules provide reusable configuration, and state tracks managed infrastructure. The typical workflow is terraform init, validate, plan, and apply, with destroy used when infrastructure needs to be removed. Terraform also supports variables, outputs, remote state backends, and lifecycle rules such as create_before_destroy, prevent_destroy, ignore_changes, and replace_triggered_by.**

---

# 45. Ready-to-Speak Project Answer

If asked:

> **“How did you use Terraform in a project?”**

Use the source's hands-on project framing:

> **I used Terraform to provision AWS infrastructure. I configured the AWS provider, defined resources such as an S3 bucket and EC2 instance, used variables to make values like region and instance type customizable, initialized Terraform, validated and planned the configuration, and then applied the changes.**

The source's hands-on project specifically describes creating an S3 bucket and EC2 instance and using variables for instance types and regions. fileciteturn3file0L282-L291

---

# 46. Complete Terraform Decision Tree

```text
What do I need?

        |
        +---- Connect to AWS/Azure/etc.?
        |         |
        |         +---- PROVIDER
        |
        +---- Define infrastructure?
        |         |
        |         +---- RESOURCE
        |
        +---- Reuse infrastructure code?
        |         |
        |         +---- MODULE
        |
        +---- Store/track infrastructure information?
        |         |
        |         +---- STATE
        |
        +---- Store state remotely?
        |         |
        |         +---- BACKEND
        |
        +---- Make configuration reusable?
        |         |
        |         +---- VARIABLE
        |
        +---- Show resource information?
        |         |
        |         +---- OUTPUT
        |
        +---- Preview changes?
        |         |
        |         +---- terraform plan
        |
        +---- Apply changes?
        |         |
        |         +---- terraform apply
        |
        +---- Remove infrastructure?
        |         |
        |         +---- terraform destroy
        |
        +---- Validate configuration?
        |         |
        |         +---- terraform validate
        |
        +---- Control resource replacement/deletion?
                  |
                  +---- LIFECYCLE
```

---

# 47. Terraform Command Cheat Sheet

| Command | Easy Meaning |
|---|---|
| `terraform --version` | Check Terraform version |
| `terraform init` | Initialize working directory |
| `terraform validate` | Validate configuration |
| `terraform plan` | Preview changes |
| `terraform apply` | Apply changes |
| `terraform destroy` | Destroy managed infrastructure |
| `terraform state list` | List state resources |
| `terraform state show <resource>` | Show resource state |
| `terraform fmt` | Format Terraform code |

---

# 48. Terraform HCL Cheat Sheet

## Provider

```hcl
provider "aws" {
  region = "us-west-2"
}
```

## Resource

```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

## Variable

```hcl
variable "instance_type" {
  description = "The instance type"
  default     = "t2.micro"
}
```

## Resource using variable

```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_type
}
```

## Output

```hcl
output "instance_public_ip" {
  value = aws_instance.my_ec2.public_ip
}
```

## Module

```hcl
module "ec2_instance" {
  source        = "./modules/ec2-instance"
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

## Backend

```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "state/terraform.tfstate"
    region = "us-west-2"
  }
}
```

## Lifecycle

```hcl
lifecycle {
  create_before_destroy = true
}
```

---

# 49. Final 30-Second Revision

```text
TERRAFORM
= Infrastructure as Code

HCL
= Configuration language

BASH
= Run Terraform commands

PROVIDER
= Connect

RESOURCE
= Infrastructure

MODULE
= Reuse

STATE
= Memory

BACKEND
= Where state is stored

VARIABLE
= Input

OUTPUT
= Information out

INIT
= Prepare

VALIDATE
= Check

PLAN
= Preview

APPLY
= Create/modify

DESTROY
= Remove

LIFECYCLE
= Control resource behavior

C
= create_before_destroy
P
= prevent_destroy
I
= ignore_changes
R
= replace_triggered_by

BEST PRACTICES
= Secure secrets + version code + terraform fmt

PROJECT
= AWS S3 + EC2 + variables + plan + apply
```

---

# 50. Final Master Memory

> **Terraform defines WHAT infrastructure you want using HCL. Providers CONNECT Terraform to platforms, resources DEFINE infrastructure, modules REUSE configuration, state REMEMBERS managed infrastructure, backends STORE that state, variables PROVIDE inputs, and outputs RETURN useful information. The normal workflow is INIT → VALIDATE → PLAN → APPLY, with DESTROY for teardown. Lifecycle uses C-P-I-R: Create before destroy, Prevent destroy, Ignore changes, Replace triggered by dependency.**

---

# 51. Source Coverage Check

This document preserves the source's full topic coverage:

- Introduction to Terraform
- Terraform definition
- Open-source IaC
- HCL
- Infrastructure automation
- Servers
- Storage
- Networks
- Declarative syntax
- Infrastructure as Code
- Platform agnostic
- AWS
- Azure
- Google Cloud
- On-premises infrastructure
- Providers
- Resources
- Modules
- State
- HCL vs Bash
- Terraform installation
- `terraform --version`
- AWS provider
- AWS credentials through AWS CLI/environment variables
- `provider.tf`
- AWS region
- Resource definition
- EC2 example
- `aws_instance`
- Resource name
- AMI
- Instance type
- `terraform init`
- Provider plugins
- `terraform plan`
- `terraform apply`
- `terraform destroy`
- `terraform validate`
- Variables
- `variables.tf`
- Variable references
- Outputs
- `outputs.tf`
- Public IP output
- Terraform state
- `terraform.tfstate`
- `terraform state list`
- `terraform state show`
- Remote state
- S3
- Modules
- Module directory structure
- Module `main.tf`
- Module `variables.tf`
- Root module usage
- Remote backends
- S3 backend
- Backend bucket/key/region
- Terraform lifecycle
- `create_before_destroy`
- Zero downtime
- Load balancers/servers
- Temporary cost increase
- Unique-name limitation
- `prevent_destroy`
- Production DB
- Critical infrastructure
- Destroy error
- `ignore_changes`
- External updates
- Autoscaling/tags
- `ignore_changes = all`
- Configuration drift risk
- `replace_triggered_by`
- AMI-triggered EC2 rebuild
- Immutable infrastructure
- Lifecycle summary
- C-P-I-R memory trick
- Lifecycle only in resource block
- Not applicable to modules
- `ignore_changes` risk
- Provider limitations
- Best practices
- Secret security
- Version control
- State handling
- `terraform fmt`
- Hands-on AWS project
- S3 bucket
- EC2 instance
- Provider configuration
- Resource blocks
- Plan/apply
- Variables for instance types and regions

---

# FINAL MASTER DIAGRAM

```text
                       TERRAFORM
                           |
                           ↓
                  Infrastructure as Code
                           |
                           ↓
                          HCL
                           |
             +-------------+-------------+
             |             |             |
             ↓             ↓             ↓
          PROVIDER      RESOURCE       MODULE
          CONNECT       INFRA          REUSE
             |             |             |
             +-------------+-------------+
                           |
                           ↓
                         STATE
                       MEMORY
                           |
                           ↓
                        BACKEND
                     STATE STORAGE
                           |
                           ↓
              INIT → VALIDATE → PLAN
                           |
                           ↓
                         APPLY
                           |
                           ↓
                    INFRASTRUCTURE
                           |
                           ↓
                       OUTPUTS
                           |
                           ↓
                       DESTROY
```

> **One-line interview memory:**
>
> **“Terraform is declarative IaC: the provider connects, resources define, modules reuse, state remembers, backend stores, variables input, outputs expose, and the workflow is init → validate → plan → apply.”**

