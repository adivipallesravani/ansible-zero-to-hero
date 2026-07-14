# Ansible Role Structure

## Objective

Understand the standard directory structure of an Ansible Role and the purpose of each directory.

---

# Standard Role Structure

```text
roles/
└── apache
    ├── defaults/
    │   └── main.yml
    ├── files/
    ├── handlers/
    │   └── main.yml
    ├── meta/
    │   └── main.yml
    ├── tasks/
    │   └── main.yml
    ├── templates/
    ├── tests/
    │   ├── inventory
    │   └── test.yml
    ├── vars/
    │   └── main.yml
    └── README.md
```

---

# Directory Overview

| Directory | Purpose |
|------------|---------|
| tasks | Contains the tasks executed by the role. |
| handlers | Contains handlers triggered by task changes. |
| files | Stores static files copied to managed nodes. |
| templates | Stores Jinja2 templates with variables. |
| vars | Contains role-specific variables. |
| defaults | Contains default variables that can be overridden. |
| meta | Stores role metadata and dependencies. |
| tests | Contains files for testing the role. |
| README.md | Documents the role. |

---

# tasks/

The `tasks/main.yml` file is the entry point of a role.

When a role is executed, Ansible automatically starts with this file.

Example:

```yaml
- name: Install Apache
  ansible.builtin.dnf:
    name: httpd
    state: present
```

---

# files/

Stores static files used by the role.

Example:

```text
roles/apache/files/index.html
```

Used with the `copy` module.

---

# templates/

Stores Jinja2 templates.

Templates allow variables to be inserted dynamically.

Example:

```apache
ServerName {{ hostname }}
Listen {{ port }}
```

Used with the `template` module.

---

# handlers/

Contains tasks that run only when notified by another task.

Example:

```yaml
- name: Restart Apache
  ansible.builtin.service:
    name: httpd
    state: restarted
```

---

# vars/

Contains variables defined specifically for the role.

Example:

```yaml
http_port: 80
```

---

# defaults/

Contains default values for variables.

These values can be overridden by variables defined in the playbook or inventory.

---

# meta/

Contains metadata about the role.

Example:

```yaml
dependencies:
  - role: common
```

---

# tests/

Contains sample inventory and test playbooks used to validate the role.

---

# Role Execution Flow

```text
Playbook
        │
        ▼
Role
        │
        ▼
tasks/main.yml
        │
        ▼
Modules
        │
        ▼
Managed Node
```

---

# Key Learnings

- Learned the standard Ansible Role structure.
- Understood the purpose of each directory.
- Learned that `tasks/main.yml` is the role entry point.
- Understood the difference between `files` and `templates`.
- Learned the purpose of `handlers`.

---

# Interview Notes

## Q1. Which file is executed first in a role?

`tasks/main.yml`

---

## Q2. What is the difference between `files` and `templates`?

`files` stores static files.

`templates` stores Jinja2 templates that support variables.

---

## Q3. Why are handlers used?

Handlers perform actions only when notified by another task, such as restarting a service after a configuration change.

---

## Q4. What is the purpose of the `defaults` directory?

It stores default variable values that can be overridden.

---

## Q5. What does the `meta` directory contain?

Role metadata such as dependencies.

---

# Next Step

The next chapter explains how to create a role using `ansible-galaxy init` and build the first custom role.
