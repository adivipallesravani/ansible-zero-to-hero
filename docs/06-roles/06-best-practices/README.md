# Ansible Role Best Practices

## Objective

Learn the recommended practices for organizing Ansible Roles and Playbooks to build reusable, maintainable, and scalable automation.

---

# Follow the Standard Role Structure

Always create roles using:

```bash
ansible-galaxy init <role_name>
```

This ensures the role follows the standard Ansible directory layout.

---

# Keep One Responsibility Per Role

Each role should perform one specific function.

Examples:

- apache
- docker
- mysql
- firewall
- users

Avoid combining unrelated tasks into a single role.

---

# Keep Playbooks Small

Playbooks should focus on orchestration.

Example:

```yaml
---
- name: Configure Web Server
  hosts: servers
  become: true

  roles:
    - apache
```

Implementation details belong inside roles.

---

# Reuse Roles

Instead of copying the same tasks into multiple playbooks, create one reusable role and use it wherever needed.

This follows the **DRY (Don't Repeat Yourself)** principle.

---

# Use Meaningful Role Names

Choose descriptive names such as:

- apache
- docker
- mysql
- users

Avoid generic names like:

- role1
- test
- sample

---

# Store Files in the Correct Directory

- Static files → `files/`
- Jinja2 templates → `templates/`
- Tasks → `tasks/main.yml`
- Handlers → `handlers/main.yml`
- Variables → `vars/` or `defaults/`

---

# Use Handlers for Service Restarts

Restart services only when required.

Example:

- Copy configuration
- Notify handler
- Restart service only if the configuration changed

---

# Document Your Roles

Include a `README.md` describing:

- Purpose
- Variables
- Usage
- Dependencies

Good documentation improves collaboration and maintenance.

---

# Test Before Production

Always validate roles in a test environment before applying them to production systems.

---

# Key Learnings

- Learned best practices for organizing Ansible roles.
- Understood the importance of reusable automation.
- Learned to keep playbooks clean and roles focused.
- Understood the DRY principle in Ansible.

---

# Interview Notes

## Q1. Why should a role have a single responsibility?

It improves readability, maintainability, and reusability.

---

## Q2. Why should playbooks remain small?

Playbooks orchestrate automation, while roles contain the implementation details.

---

## Q3. What is the DRY principle?

DRY stands for **Don't Repeat Yourself**. Reusable roles prevent code duplication across multiple projects.

---

## Q4. Why use meaningful role names?

Meaningful names make projects easier to understand and maintain.

---

## Q5. Why should roles be tested before production?

Testing helps identify issues early and reduces the risk of failures in production environments.

---

# Next Step

The next chapter introduces Ansible Variables and Variable Precedence.
