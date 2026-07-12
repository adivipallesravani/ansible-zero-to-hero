# Ansible Inventory

## Objective

Understand what an Ansible inventory is, why it is required, and how it is used to organize and manage one or more managed nodes.

---

## What is an Inventory?

Ansible Inventory is a file that contains information about the managed nodes. It tells Ansible which hosts to connect to and allows them to be organized into logical groups.

Without an inventory, Ansible does not know which systems should receive automation tasks.

---

## Why do we need an Inventory?

Imagine an organization with hundreds of Linux servers.

Instead of specifying the IP address every time a command is executed, all managed nodes are maintained in a single inventory file.

Benefits include:

- Centralized host management
- Host grouping
- Easier automation
- Improved scalability

---

## Inventory Architecture

```text
Controller Node

Inventory File
│
├── webservers
│      ├── 192.168.29.90
│      └── 192.168.29.91
│
└── dbservers
       └── 192.168.29.100

        │
        ▼

Managed Nodes
```

The inventory acts as a bridge between the controller node and the managed nodes by defining where Ansible should execute tasks.

---

## Inventory Types

### Static Inventory

A manually maintained inventory file.

Example:

```ini
[servers]
192.168.29.90
```

---

### Dynamic Inventory

Automatically discovers hosts from cloud providers such as AWS, Azure, or GCP.

Dynamic inventory is commonly used in production environments where servers are created and removed automatically.

---

## Inventory File Example

```ini
[servers]
192.168.29.90

[web]
192.168.29.91

[database]
192.168.29.100
```

---

## Inventory Groups

Inventory groups allow multiple managed nodes to be organized logically.

Example:

```ini
[web]
web01
web02

[database]
db01
```

Instead of executing commands on individual hosts, commands can be executed on an entire group.

---

## Verification

| Check | Command | Expected Result |
|-------|---------|-----------------|
| Verify Inventory | `cat inventory` | Displays configured hosts |
| Ping Managed Nodes | `ansible servers -i inventory -m ping` | Returns `SUCCESS` with `pong` |

---

## Common Mistakes

- Incorrect IP address
- Wrong inventory file path
- Typographical errors in group names
- Missing SSH connectivity
- Incorrect username for managed nodes

---

## Troubleshooting

### Host unreachable

Possible reasons:

- Incorrect IP address
- Network connectivity issue
- SSH service not running

---

### No hosts matched

Possible reasons:

- Wrong inventory group
- Inventory file not specified
- Typographical error in host group name

---

## Key Learnings

- Learned the purpose of an Ansible Inventory.
- Understood the difference between static and dynamic inventory.
- Organized managed nodes into logical groups.
- Verified connectivity using the inventory file.

---

## Interview Notes

### Q1. What is an Ansible Inventory?

An inventory is a file that contains information about managed nodes. It tells Ansible where to execute automation tasks.

---

### Q2. Why is an Inventory required?

Without an inventory, Ansible does not know which managed nodes should receive automation tasks.

---

### Q3. What is the difference between Static and Dynamic Inventory?

Static inventory is manually maintained.

Dynamic inventory automatically discovers hosts from cloud platforms such as AWS, Azure, or GCP.

---

### Q4. Can a managed node belong to multiple groups?

Yes.

A managed node can belong to multiple inventory groups simultaneously.

---

### Q5. What happens if the inventory file contains an incorrect IP address?

Ansible will fail to connect and report the host as unreachable.

---

## References

- Official Ansible Documentation

---

## Next Step

The next chapter explains Ansible Ad Hoc Commands and how to execute one-time automation tasks on managed nodes.
