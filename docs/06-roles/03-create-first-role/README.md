# Create Your First Ansible Role

## Objective

Learn how to create an Ansible Role using the `ansible-galaxy init` command and understand how Ansible generates the standard role structure.

---

# What is `ansible-galaxy init`?

The `ansible-galaxy init` command creates a new role with the standard directory structure recommended by Ansible.

Instead of creating folders manually, Ansible generates them automatically.

---

# Syntax

```bash
ansible-galaxy init <role_name>
```

Example:

```bash
ansible-galaxy init apache
```

---

# Generated Role Structure

```text
roles/
└── apache
    ├── defaults/
    ├── files/
    ├── handlers/
    ├── meta/
    ├── tasks/
    ├── templates/
    ├── tests/
    ├── vars/
    └── README.md
```

---

# Adding Tasks

Move the tasks from the playbook into:

```text
roles/apache/tasks/main.yml
```

Example:

```yaml
---
- name: Install Apache
  ansible.builtin.dnf:
    name: httpd
    state: present

- name: Copy index.html
  ansible.builtin.copy:
    src: index.html
    dest: /var/www/html/index.html
    owner: root
    group: root
    mode: "0644"

- name: Start and Enable Apache
  ansible.builtin.service:
    name: httpd
    state: started
    enabled: true
```

---

# Moving Static Files

Move static files into the role.

Example:

```text
roles/apache/files/index.html
```

The `copy` module automatically searches the role's `files` directory.

---

# Advantages

- Standard directory structure
- Faster role creation
- Reduces manual effort
- Encourages best practices
- Makes roles reusable

---

# Key Learnings

- Learned how to create a role.
- Understood the purpose of `ansible-galaxy init`.
- Moved tasks into `tasks/main.yml`.
- Moved static files into `files/`.

---

# Interview Notes

## Q1. What does `ansible-galaxy init` do?

It creates a new role with the standard Ansible directory structure.

---

## Q2. Why use `ansible-galaxy init` instead of creating folders manually?

It ensures the role follows the recommended structure and reduces manual setup.

---

## Q3. Where are the executable tasks stored in a role?

`tasks/main.yml`

---

# Next Step

The next chapter explains how to use a role inside a playbook.
