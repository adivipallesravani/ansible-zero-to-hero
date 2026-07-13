# First Ansible Playbook

## Objective

Understand how to write, execute, and verify a basic Ansible Playbook using the built-in Ping module.

---

## What is an Ansible Playbook?

An Ansible Playbook is a YAML file that defines automation tasks to be executed on one or more managed nodes. Playbooks provide a reusable and maintainable way to automate infrastructure and application management.

---

## Playbook Used

```yaml
---
- name: Test Ansible Connectivity
  hosts: servers

  tasks:
    - name: Ping managed nodes
      ansible.builtin.ping:
```

---

## Understanding the Playbook

### `---`

Marks the beginning of a YAML document.

---

### `- name: Test Ansible Connectivity`

Defines the name of the Play. This name is displayed when the playbook is executed.

---

### `hosts: servers`

Specifies the target hosts. The `servers` group is defined in the inventory file.

---

### `tasks:`

Defines the list of tasks to execute on the managed nodes.

---

### `- name: Ping managed nodes`

Defines the name of the Task.

---

### `ansible.builtin.ping:`

Uses the built-in Ping module to verify Ansible connectivity with the managed node.

Unlike the Linux `ping` command, the Ansible Ping module checks whether Ansible can successfully connect to the managed node and execute a module.

---

## Playbook Execution Flow

```text
Controller Node
        │
        ▼
Read Playbook
        │
        ▼
Read Inventory
        │
        ▼
Connect to Managed Node using SSH
        │
        ▼
Gather Facts
        │
        ▼
Execute Ping Module
        │
        ▼
Display Play Recap
```

---

## Running the Playbook

```bash
ansible-playbook -i inventory playbooks/ping.yml
```

---

## Output

```text
PLAY [Test Ansible Connectivity] ****************************************

TASK [Gathering Facts] **************************************************
ok: [192.168.29.90]

TASK [Ping managed nodes] ***********************************************
ok: [192.168.29.90]

PLAY RECAP **************************************************************
192.168.29.90 : ok=2 changed=0 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0
```

---

## Understanding the Output

### PLAY

Displays the name of the Play currently being executed.

---

### TASK [Gathering Facts]

Before executing user-defined tasks, Ansible automatically collects information about the managed node, including:

- Hostname
- Operating System
- IP Address
- Memory
- CPU
- Network Information

---

### TASK [Ping managed nodes]

Executes the Ansible Ping module to verify communication with the managed node.

---

### PLAY RECAP

Displays a summary of the playbook execution.

| Field | Meaning |
|--------|---------|
| ok | Number of successfully executed tasks |
| changed | Number of tasks that modified the system |
| unreachable | Number of unreachable hosts |
| failed | Number of failed tasks |
| skipped | Number of skipped tasks |
| rescued | Number of rescued tasks |
| ignored | Number of ignored failures |

---

## Ad Hoc Command vs Playbook

| Ad Hoc Command | Playbook |
|---------------|----------|
| Executes a single task | Executes one or more tasks |
| Command-line based | YAML file based |
| Suitable for quick tasks | Suitable for repeatable automation |
| Difficult to maintain | Easy to maintain and version control |

---

## Key Learnings

- Wrote the first Ansible Playbook.
- Understood the structure of a Playbook.
- Learned the purpose of Plays, Tasks, and Modules.
- Executed a Playbook using `ansible-playbook`.
- Understood the meaning of the Play Recap.
- Learned that Ansible automatically gathers facts before executing tasks.

---

## Interview Notes

### Q1. What is an Ansible Playbook?

An Ansible Playbook is a YAML file that contains one or more Plays used to automate tasks on managed nodes.

---

### Q2. What is the purpose of the Ping module?

The Ping module verifies that Ansible can connect to the managed node and execute modules successfully.

---

### Q3. What is the purpose of Gathering Facts?

Gathering Facts collects system information about the managed node before executing tasks.

---

### Q4. What does `ok=2` indicate?

It indicates that two tasks completed successfully: Gathering Facts and the Ping task.

---

### Q5. Why is `changed=0`?

The Ping module only verifies connectivity and does not modify the managed node.

---

### Q6. What is the difference between an Ad Hoc command and a Playbook?

Ad Hoc commands are used for one-time tasks, whereas Playbooks are reusable YAML files designed for repeatable automation.

---

## Next Step

The next chapter demonstrates how to automate Apache installation and deploy a static web page using an Ansible Playbook.
