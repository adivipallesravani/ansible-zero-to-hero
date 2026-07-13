# YAML Basics

## Objective

Understand YAML syntax and data structures used in Ansible playbooks.

---

## What is YAML?

YAML (YAML Ain't Markup Language) is a human-readable data serialization language used to represent structured data. Ansible uses YAML to define playbooks because it is simple, readable, and easy to maintain.

---

## Why does Ansible use YAML?

Ansible uses YAML because it is:

- Human-readable
- Easy to write and maintain
- Supports nested data structures
- Simpler than JSON or XML for configuration files

---

## YAML Rules

### 1. Indentation

YAML uses **spaces** to define the hierarchy of data.

> **Note:** Use spaces instead of tabs.

Correct:

```yaml
person:
  name: John
  age: 30
```

Incorrect:

```yaml
person:
name: John
age: 30
```

---

### 2. Key-Value Pair

A key-value pair stores a single piece of information.

Example:

```yaml
name: Sravani
course: Ansible
experience: 3
```

---

### 3. List

A list stores multiple values under a single key.

Example:

```yaml
packages:
  - git
  - vim
  - httpd
```

---

### 4. Dictionary

A dictionary stores related information using key-value pairs.

Example:

```yaml
server:
  hostname: web01
  ip: 192.168.29.90
  os: CentOS
```

---

### 5. List of Dictionaries

A list of dictionaries stores multiple objects, where each object contains its own key-value pairs.

Example:

```yaml
servers:
  - hostname: web01
    ip: 192.168.29.90
    os: CentOS

  - hostname: web02
    ip: 192.168.29.91
    os: Ubuntu
```

---

### 6. Comments

Comments begin with the `#` symbol.

Example:

```yaml
# Install Apache
package: httpd
```

---

## YAML Data Types

### String

```yaml
name: Sravani
```

### Number

```yaml
experience: 3
```

### Boolean

```yaml
enabled: true
production: false
```

---

## Why YAML is Important in Ansible

Every Ansible Playbook is written in YAML. Understanding YAML is essential before writing playbooks because playbooks use YAML syntax to define plays, tasks, variables, and modules.

---

## Key Learnings

- Understood what YAML is.
- Learned why Ansible uses YAML.
- Learned YAML indentation rules.
- Understood key-value pairs.
- Learned Lists and Dictionaries.
- Understood List of Dictionaries.
- Learned basic YAML data types.

---

## Interview Notes

### Q1. What is YAML?

YAML is a human-readable data serialization language used to represent structured data.

---

### Q2. Is YAML a programming language?

No. YAML is a data serialization language, not a programming language.

---

### Q3. Why does Ansible use YAML?

Because YAML is simple, human-readable, and easy to maintain.

---

### Q4. What is the difference between a List and a Dictionary?

A List stores multiple values using the `-` symbol, whereas a Dictionary stores related data as key-value pairs.

---

### Q5. What is a List of Dictionaries?

A List of Dictionaries stores multiple objects, where each object contains multiple key-value pairs.

---

## Next Step

The next chapter explains the structure of an Ansible Playbook, including Plays, Tasks, Modules, and Collections.
