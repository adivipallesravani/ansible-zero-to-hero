# Ansible Playbook Structure

## Objective

Understand the building blocks of an Ansible Playbook, including Plays, Tasks, Modules, and Collections.

---

## What is a Playbook?

A Playbook is a YAML file that automates tasks on one or more managed nodes. It contains one or more Plays and defines the desired state of the managed infrastructure.

Example:

```text
install-apache.yml
```

---

## What is a Play?

A Play is a section within a Playbook that maps a group of managed hosts to a set of tasks.

Example:

```yaml
- name: Configure Web Servers
  hosts: webservers
```

A Playbook can contain one or more Plays.

---

## What is a Task?

A Task is a single unit of work performed on managed nodes. Tasks are executed sequentially from top to bottom and use Ansible modules to perform specific actions.

Example:

```yaml
tasks:
  - name: Install Apache
```

---

## What is a Module?

A Module is a reusable piece of code that performs a specific operation on a managed node, such as installing packages, copying files, managing users, or controlling services.

Common modules include:

- ansible.builtin.ping
- ansible.builtin.copy
- ansible.builtin.file
- ansible.builtin.service
- ansible.builtin.user
- ansible.builtin.yum
- ansible.builtin.apt

Example:

```yaml
ansible.builtin.yum:
  name: httpd
  state: present
```

---

## What is a Collection?

A Collection is a packaged distribution of Ansible content, including modules, roles, plugins, and documentation. Collections help organize and reuse Ansible content.

Example:

```text
ansible.builtin
community.general
```

---

## Ansible Playbook Hierarchy

```text
Playbook
│
├── Play
│     ├── Hosts
│     ├── Become
│     └── Tasks
│
├── Task
│     └── Module
│
└── Collections
```

---

## Playbook Execution Flow

```text
Playbook
    │
    ▼
Play
    │
    ▼
Hosts
    │
    ▼
Tasks
    │
    ▼
Modules
    │
    ▼
Managed Node
```

---

## Ad Hoc Commands vs Playbooks

| Ad Hoc Commands | Playbooks |
|-----------------|-----------|
| Execute one-time tasks | Automate repeatable tasks |
| Run from the command line | Written in YAML files |
| Best for quick operations | Best for reusable automation |
| Difficult to maintain | Easy to maintain and version control |

---

## Why Use Playbooks?

- Reusable automation
- Easy to maintain
- Version controlled
- Human-readable
- Idempotent
- Suitable for complex workflows

---

## Key Learnings

- Understood the structure of an Ansible Playbook.
- Learned the relationship between Plays, Tasks, and Modules.
- Learned the purpose of Collections.
- Compared Ad Hoc Commands with Playbooks.

---

## Interview Notes

### Q1. What is a Playbook?

A Playbook is a YAML file that contains one or more Plays used to automate tasks on managed nodes.

---

### Q2. What is a Play?

A Play maps a group of hosts to a list of tasks.

---

### Q3. What is a Task?

A Task is a single action executed on managed nodes using an Ansible module.

---

### Q4. What is a Module?

A Module is a reusable unit of code that performs a specific operation on a managed node.

---

### Q5. What is a Collection?

A Collection is a package containing Ansible modules, roles, plugins, and other reusable content.

---

### Q6. What is the difference between Ad Hoc Commands and Playbooks?

Ad Hoc Commands are used for one-time administrative tasks, whereas Playbooks are reusable YAML files used for repeatable automation.

---

### Q7. What is idempotency in Ansible?

Idempotency means running the same Playbook multiple times produces the same desired state. Ansible changes the system only when necessary.

---

## Next Step

The next chapter explains how to write and execute your first Ansible Playbook.
