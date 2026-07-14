# Using Roles in a Playbook

## Objective

Learn how to use Ansible Roles inside a playbook and understand how Ansible executes them.

---

# Why Use Roles in a Playbook?

A playbook defines **where** automation should run, while roles define **what** automation should perform.

This separation makes playbooks simple and roles reusable.

---

# Example Playbook

```yaml
---
- name: Configure Web Server
  hosts: servers
  become: true

  roles:
    - apache
```

---

# Execution Flow

```text
Playbook
        │
        ▼
Target Hosts
        │
        ▼
Become Root
        │
        ▼
Load Apache Role
        │
        ▼
tasks/main.yml
        │
        ▼
Task 1
        │
        ▼
Task 2
        │
        ▼
Task 3
```

---

# Role Execution Order

If multiple roles are defined:

```yaml
roles:
  - common
  - apache
  - docker
```

Ansible executes them sequentially:

1. common
2. apache
3. docker

Each role is completed before the next role starts.

---

# Benefits

- Cleaner playbooks
- Reusable automation
- Easier maintenance
- Better organization
- Scalable for large projects

---

# Key Learnings

- Learned how to call roles from a playbook.
- Understood the responsibility of a playbook.
- Understood the responsibility of a role.
- Learned that roles execute sequentially.

---

# Interview Notes

## Q1. Can a playbook contain multiple roles?

Yes. A playbook can contain one or more roles.

---

## Q2. How are roles executed?

Roles are executed sequentially in the order they are listed.

---

## Q3. Does a role contain hosts?

No. The playbook defines the target hosts. A role contains only the implementation.

---

## Q4. Can the same role be used in multiple playbooks?

Yes. Roles are designed to be reusable across different playbooks.

---

# Next Step

The next chapter introduces Ansible Galaxy and explains how to search, install, initialize, and import roles.
