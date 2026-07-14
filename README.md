# 🚀 Ansible Zero to Hero

A hands-on repository documenting my journey of learning **Ansible** from the fundamentals to advanced automation concepts through practical labs, real-world examples, and interview-focused documentation.

This repository focuses on learning Ansible by performing real hands-on exercises instead of only studying theory.

---

# 📖 About This Repository

This repository includes:

- YAML Fundamentals
- Ansible Playbooks
- Ansible Roles
- Ansible Galaxy
- Infrastructure Automation
- Real Lab Setup
- Troubleshooting
- Interview Questions
- Best Practices

The objective is to build strong practical knowledge of Ansible while creating a reusable reference for interviews and future projects.

---

# 🛠 Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Windows 11 |
| Controller Node | Ubuntu 24.04 (WSL2) |
| Managed Node | CentOS Stream 9 |
| Automation Tool | Ansible |
| Version Control | Git & GitHub |
| Communication | SSH Passwordless Authentication |
| Virtualization | Oracle VirtualBox |

---

# 📂 Repository Structure

```text
ansible-zero-to-hero/
│
├── ansible.cfg
├── inventory
│
├── docs/
│   ├── 01-lab-setup/
│   ├── 02-ssh/
│   ├── 03-inventory/
│   ├── 04-adhoc-commands/
│   │
│   ├── 05-playbooks/
│   │   ├── 01-yaml-basics/
│   │   ├── 02-playbook-structure/
│   │   ├── 03-first-playbook/
│   │   └── 04-apache-deployment/
│   │
│   └── 06-roles/
│       ├── 01-introduction-to-roles/
│       ├── 02-role-structure/
│       ├── 03-create-first-role/
│       ├── 04-using-roles/
│       ├── 05-ansible-galaxy/
│       └── 06-best-practices/
│
├── playbooks/
│   ├── ping.yml
│   ├── apache.yml
│   └── site.yml
│
├── roles/
│   └── apache/
│
├── examples/
├── files/
├── screenshots/
└── README.md
```

---

# 📚 Learning Roadmap

- [x] Lab Setup
- [x] SSH Passwordless Authentication
- [x] Inventory
- [x] Ad Hoc Commands
- [x] YAML Basics
- [x] Playbook Structure
- [x] First Playbook
- [x] Apache Deployment
- [x] Ansible Roles
- [x] Ansible Galaxy
- [x] Role Best Practices
- [ ] Variables
- [ ] Jinja2 Templates
- [ ] Variable Precedence
- [ ] Conditionals
- [ ] Loops
- [ ] Error Handling
- [ ] Ansible Vault
- [ ] Policy as Code
- [ ] Network Automation
- [ ] Ansible Automation Platform (Tower)

---

# 📖 Topics Covered

## Fundamentals

- Lab Setup
- SSH Passwordless Authentication
- Inventory
- Ad Hoc Commands
- YAML Basics
- Playbook Structure
- First Playbook
- Apache Deployment
- Ansible Roles
- Ansible Galaxy
- Role Best Practices

---

# 🎯 Learning Goals

- Understand Ansible architecture.
- Build reusable automation using Playbooks and Roles.
- Learn Infrastructure Automation.
- Follow Ansible best practices.
- Prepare for DevOps interviews.

---

# 🚀 Practical Labs Completed

- Configured Ubuntu WSL as the Ansible Controller.
- Configured CentOS Stream as the Managed Node.
- Established SSH passwordless authentication.
- Created and managed Ansible Inventory.
- Executed Ad Hoc Commands.
- Wrote and executed Ansible Playbooks.
- Installed Apache (`httpd`) using Ansible.
- Deployed a static website using the `copy` module.
- Enabled and started the Apache service.
- Configured the CentOS firewall to allow HTTP traffic.
- Created reusable Apache Roles.
- Executed role-based automation using `site.yml`.
- Created roles using `ansible-galaxy init`.

---

# 📊 Progress

| Chapter | Status |
|----------|--------|
| Lab Setup | ✅ Completed |
| SSH | ✅ Completed |
| Inventory | ✅ Completed |
| Ad Hoc Commands | ✅ Completed |
| Playbooks | ✅ Completed |
| Roles | ✅ Completed |
| Variables | ⏳ Next |

---

# 💻 Technologies Used

- Linux
- WSL2
- CentOS Stream
- Ansible
- Git
- GitHub
- SSH
- VirtualBox

---

# 📌 Repository Highlights

- Real-world hands-on labs
- Production-style project structure
- YAML examples
- Playbooks
- Roles
- Ansible Galaxy
- Architecture diagrams
- Troubleshooting
- Interview questions
- Best practices

---

# 🤝 Contributing

This repository is maintained as part of my personal learning journey.

Suggestions and improvements are always welcome.

---

# ⭐ Support

If you find this repository useful, consider giving it a ⭐ on GitHub.
