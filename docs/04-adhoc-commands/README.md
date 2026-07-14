# Ansible Ad Hoc Commands

## Objective

Understand how to execute one-time administrative tasks on managed nodes using Ansible Ad Hoc commands without creating playbooks.

---

# What are Ad Hoc Commands?

Ad Hoc commands are one-line Ansible commands used to perform quick administrative tasks on managed nodes.

They are commonly used for:

- Verifying connectivity
- Gathering system information
- Installing packages
- Managing services
- Copying files
- Creating users
- Managing directories

---

# Syntax

```bash
ansible <host-pattern> -i <inventory-file> -m <module> -a "<arguments>"
```

Example:

```bash
ansible servers -i inventory -m ping
```

---

# Ad Hoc Command Flow

```text
Controller Node
      │
      ▼
Ansible Command
      │
      ▼
Inventory
      │
      ▼
Managed Node
      │
      ▼
Requested Module Executes
```

---

# Commonly Used Modules

## 1. Ping Module

### Purpose

Verifies Ansible connectivity with managed nodes.

### Command

```bash
ansible servers -i inventory -m ping
```

### Output

```text
192.168.29.90 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

### Explanation

The `ping` module checks whether Ansible can successfully communicate with the managed node over SSH. It does **not** perform an ICMP ping.

---

## 2. Command Module

### Purpose

Executes commands directly on the managed node.

### Command

```bash
ansible servers -i inventory -m command -a "hostname"
```

### Output

```text
192.168.29.90 | CHANGED | rc=0 >>
sravani
```

### Explanation

The `command` module executes commands directly without invoking a shell.

---

## 3. Shell Module

### Purpose

Executes shell commands on the managed node.

### Command

```bash
ansible servers -i inventory -m shell -a "df -h"
```

### Output

```text
Filesystem           Size  Used Avail Use% Mounted on
/dev/mapper/cs-root   17G  5.5G   12G  32% /
/dev/sda1            960M  495M  466M  52% /boot
```

### Explanation

The `shell` module executes commands through a shell and supports shell features such as pipes (`|`), redirection (`>`), and environment variables.

---

## 4. Copy Module

### Purpose

Copies files from the controller node to the managed node.

### Command

```bash
ansible servers -i inventory -m copy -a "src=test.txt dest=/tmp/test.txt"
```

### Output

```text
192.168.29.90 | CHANGED => {
    "changed": true,
    "dest": "/tmp/test.txt",
    "state": "file"
}
```

### Explanation

The `copy` module transfers files from the controller node to the managed node.

---

## 5. File Module

### Purpose

Creates or manages files and directories.

### Command

```bash
ansible servers -i inventory -m file -a "path=/tmp/demo state=directory"
```

### Output

```text
192.168.29.90 | CHANGED => {
    "changed": true,
    "path": "/tmp/demo",
    "state": "directory"
}
```

### Explanation

The `file` module creates, removes, or modifies files and directories.

---

## 6. Package Module

### Purpose

Installs software packages on managed nodes.

### Command

```bash
ansible servers -i inventory -b -m dnf -a "name=httpd state=present"
```

### Output

```text
192.168.29.90 | CHANGED => {
    "changed": true,
    "name": "httpd",
    "state": "present"
}
```

### Verification

```bash
ansible servers -i inventory -m command -a "rpm -q httpd"
```

### Example Output

```text
192.168.29.90 | CHANGED | rc=0 >>
httpd-2.4.62-14.el9.x86_64
```

### Explanation

The `dnf` module installs and manages software packages on CentOS Stream 9 and other RHEL-based Linux distributions. If the package is already installed, Ansible reports `ok` without making any changes, demonstrating idempotent behavior.

---

## 7. Service Module

### Purpose

Starts, stops, restarts, or enables services.

### Command

```bash
ansible servers -i inventory -K -b -m service -a "name=httpd state=started enabled=yes"
```

### Output

```text
192.168.29.90 | SUCCESS => {
    "changed": true,
    "name": "httpd",
    "state": "started"
}
```

### Explanation

The `service` module manages system services. The `-b` option enables privilege escalation (sudo), and `-K` prompts for the sudo password.

---

## 8. User Module

### Purpose

Creates user accounts on the managed node.

### Command

```bash
ansible servers -i inventory -K -b -m user -a "name=developer state=present"
```

### Output

```text
192.168.29.90 | CHANGED => {
    "changed": true,
    "name": "developer",
    "state": "present",
    "home": "/home/developer"
}
```

### Verification

```bash
ansible servers -i inventory -m command -a "id developer"
```

```text
uid=1008(developer) gid=1012(developer) groups=1012(developer)
```

### Explanation

The `user` module creates and manages Linux user accounts. Administrative privileges are required, so `-b` and `-K` are used.

---

# Verification

| Module | Status |
|---------|--------|
| Ping | ✅ Successful |
| Command | ✅ Successful |
| Shell | ✅ Successful |
| Copy | ✅ Successful |
| File | ✅ Successful |
| Package | ✅ Successful |
| Service | ✅ Successful |
| User | ✅ Successful |

---

# Common Mistakes

- Incorrect inventory file path.
- Running commands without SSH connectivity.
- Forgetting to use `-b` for privileged tasks.
- Forgetting `-K` when sudo requires a password.
- Using the wrong package manager for the operating system.
- Trying to copy a file that does not exist on the controller node.

---

# Troubleshooting

## Copy Module Failed

### Error

```text
Could not find or access 'test.txt'
```

### Reason

The source file did not exist on the controller node.

### Solution

Create the file before running the `copy` module.

---

## Missing sudo password

### Error

```text
Missing sudo password
```

### Reason

Privilege escalation was requested without providing the sudo password.

### Solution

Use the `-K` option together with `-b`.

---

# Key Learnings

- Executed Ansible Ad Hoc commands from the controller node.
- Verified connectivity using the Ping module.
- Executed remote commands using the Command and Shell modules.
- Copied files using the Copy module.
- Created directories using the File module.
- Installed software packages using the DNF module.
- Managed services using the Service module.
- Created Linux users using the User module.
- Learned when privilege escalation (`-b`) and sudo password (`-K`) are required.

---

# Interview Notes

## Q1. What are Ad Hoc Commands?

Ad Hoc commands are one-time Ansible commands used to execute administrative tasks without writing playbooks.

---

## Q2. What is the difference between the Command and Shell modules?

The `command` module executes commands directly without using a shell.

The `shell` module executes commands through a shell and supports pipes, redirection, and environment variables.

---

## Q3. Why are `-b` and `-K` used?

- `-b` enables privilege escalation (become/sudo).
- `-K` prompts for the sudo password when required.

---

## Q4. Why did the Copy module initially fail?

Because the source file (`test.txt`) did not exist on the controller node.

---

## Q5. Which module is used to install packages on CentOS Stream 9?

The `dnf` module is commonly used to install and manage software packages on CentOS Stream 9.

---

## Q6. Why are Playbooks preferred over Ad Hoc Commands?

Playbooks are reusable, version-controlled, and better suited for complex automation.

---

# References

- Official Ansible Documentation

---

# Next Step

The next chapter covers Ansible Playbooks, where repeatable automation tasks are written using YAML.
