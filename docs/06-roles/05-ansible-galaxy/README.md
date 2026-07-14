# Ansible Galaxy

## Objective

Understand what Ansible Galaxy is, how it helps reuse automation, and learn the common commands used to create, search, install, and share roles.

---

# What is Ansible Galaxy?

Ansible Galaxy is the official repository for Ansible Roles and Collections.

It allows users to search, download, share, and reuse automation created by the Ansible community and organizations.

Instead of creating every role from scratch, you can use existing, well-tested roles.

---

# Why Use Ansible Galaxy?

- Saves development time.
- Encourages code reuse.
- Provides community-maintained roles.
- Follows best practices.
- Makes automation faster and more consistent.

---

# Common Commands

## Create a Role

```bash
ansible-galaxy init apache
```

Creates a new role with the standard directory structure.

---

## Search Roles

```bash
ansible-galaxy role search nginx
```

Searches Ansible Galaxy for publicly available roles.

---

## Install a Role

```bash
ansible-galaxy role install geerlingguy.apache
```

Downloads and installs a role from Ansible Galaxy.

---

## List Installed Roles

```bash
ansible-galaxy role list
```

Displays all installed roles.

---

## Import a Role

```bash
ansible-galaxy role import <github_username> <repository_name>
```

Imports a GitHub role into Ansible Galaxy, making it available for others to use.

---

# When to Use Ansible Galaxy

Use Galaxy when you need common automation such as:

- Apache
- Nginx
- Docker
- Kubernetes
- MySQL

Community roles reduce the need to write automation from scratch.

---

# When to Create Your Own Role

Create your own role when:

- Your organization has custom requirements.
- Internal standards must be followed.
- The required automation is not available publicly.

---

# Key Learnings

- Learned the purpose of Ansible Galaxy.
- Learned how to create, search, install, and import roles.
- Understood when to use community roles.
- Understood when to create custom roles.

---

# Interview Notes

## Q1. What is Ansible Galaxy?

Ansible Galaxy is the official repository for Ansible Roles and Collections.

---

## Q2. Why use Ansible Galaxy?

It provides reusable, community-maintained automation, reducing development time and improving consistency.

---

## Q3. Which command creates a role?

```bash
ansible-galaxy init <role_name>
```

---

## Q4. Which command installs a role?

```bash
ansible-galaxy role install <role_name>
```

---

## Q5. When would you create your own role instead of using Galaxy?

When the organization requires custom automation or internal standards that are not met by public roles.

---

# Next Step

The next chapter covers best practices for organizing Ansible roles and playbooks.
