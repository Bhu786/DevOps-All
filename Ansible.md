from pathlib import Path

md_path = Path("/mnt/data/Ansible_Interview_Notes_Start_to_End.md")

md = r"""# ANSIBLE — INTERVIEW NOTES

**Start-to-End • Simple to Learn • Easy to Remember • Interview Ready**

> **IMPORTANT:** This version keeps the complete content of the uploaded PATHNEX Ansible PDF, but reorganizes it into simpler interview-friendly language, memory tricks, and clear examples.

The source covers Ansible definition, why to use it, components, workflow, playbooks, inventory, modules, roles, control node, managed nodes, use cases, examples, benefits, and conclusion.

> **MASTER MEMORY TRICK**
>
> **CONTROL NODE → INVENTORY → PLAYBOOK → MODULES → MANAGED NODES → RESULT**

---

# 1. What is Ansible?

Ansible is an **open-source automation tool** used for:

- Configuration management
- Application deployment
- Task automation

It automates repetitive IT work such as:

- Installing software
- Configuring servers
- Managing many machines

It can be used in:

- On-premises environments
- Cloud environments
- Hybrid environments

### Interview Answer

> **Ansible is an open-source automation tool used for configuration management, application deployment, and task automation. It is agentless and normally communicates with Linux/Unix machines using SSH and Windows machines using WinRM.**

### Memory Trick

**Ansible = AUTOMATE + CONFIGURE + DEPLOY + NO AGENT**

---

# 2. Why Use Ansible?

## 2.1 Simplifies Complex Tasks

Ansible automates tasks that would otherwise require manual intervention.

Examples:

- Setting up a web server
- Updating systems
- Deploying applications

## 2.2 Consistency

Ansible ensures that systems are configured in the same way.

This helps reduce:

- Human errors
- Configuration differences
- Repetitive manual work

## 2.3 Scalability

Ansible can manage:

- One system
- Hundreds of systems
- Thousands of systems

The same configuration can be reused across many machines.

## 2.4 No Agent Required

Ansible does not require a special Ansible agent to be installed on target machines.

Communication:

- **Linux/Unix → SSH**
- **Windows → WinRM**

### Interview Answer

> **I use Ansible when I need the same configuration or operational task to be performed consistently across multiple servers. Its agentless approach makes setup simple because the target machines do not need a dedicated Ansible agent.**

### Memory Trick

**Why Ansible? → EASY + CONSISTENT + SCALABLE + AGENTLESS**

---

# 3. Basic Components of Ansible

The important components covered in the source are:

1. Playbooks
2. Inventory
3. Modules
4. Roles

---

## 3.1 Playbooks

Playbooks are the **core files** where we define the tasks Ansible should execute.

They are written in **YAML**.

YAML is:

- Human-readable
- Easy to understand

A playbook contains one or more **plays**.

A play defines:

- What actions should be performed
- On which group of systems

### Interview Answer

> **A playbook is a YAML file that describes the desired sequence of tasks and the hosts on which those tasks should run.**

### Memory Trick

**Playbook = WHAT TO DO + WHERE TO DO IT**

---

## 3.2 Inventory

An inventory is the list of:

- Servers
- Hosts
- IP addresses
- Hostnames

that Ansible manages.

Inventory can be:

### Static Inventory

A simple file containing hostnames or IP addresses.

Example:

```ini
[webservers]
server1.example.com
server2.example.com
