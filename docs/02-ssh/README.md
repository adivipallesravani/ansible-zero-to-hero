# SSH Passwordless Authentication

## Objective

Understand how SSH enables secure, passwordless communication between the Ansible controller node and managed nodes using public key authentication.

---

## Why SSH?

Ansible is an agentless automation tool. Instead of installing software on every managed node, it uses SSH to securely connect from the controller node to the managed node and execute commands remotely.

SSH provides:

- Secure encrypted communication
- User authentication using passwords or SSH keys
- Remote command execution

---

## Password Authentication vs SSH Key Authentication

### Password Authentication

The user enters a password every time an SSH connection is established.

### SSH Key Authentication

SSH key authentication uses a public-private key pair.

- The private key remains securely on the controller node.
- The public key is copied to the managed node using `ssh-copy-id`.
- During login, the managed node verifies that the client owns the matching private key.
- If the verification succeeds, the user is authenticated without entering a password.

---

## SSH Authentication Flow

The following diagram illustrates how SSH key-based authentication works.

```text
Controller Node (WSL)

├── Private Key (id_ed25519)
└── Public Key (id_ed25519.pub)
        │
        │ ssh-copy-id
        ▼
Managed Node (CentOS)

~/.ssh/authorized_keys
        │
        ▼
Stores Public Key
```

The controller node generates a public-private key pair using `ssh-keygen`. The public key is copied to the managed node using `ssh-copy-id` and stored in the `authorized_keys` file. During authentication, the managed node verifies that the controller possesses the matching private key before allowing access.

---

## SSH Key-Based Authentication Setup

### Step 1: Generate an SSH Key Pair

Generate a new SSH key pair on the controller node.

```bash
ssh-keygen
```

**Purpose**

Creates a public-private key pair used for SSH authentication.

---

### Step 2: Copy the Public Key to the Managed Node

Copy the public key to the managed node.

```bash
ssh-copy-id <username>@<managed-node-ip>
```

**Example**

```bash
ssh-copy-id sravani@192.168.29.90
```

**Purpose**

Copies the public key to the managed node and stores it in the `~/.ssh/authorized_keys` file.

---

### Step 3: Verify Passwordless SSH

Verify that passwordless authentication is working.

```bash
ssh <username>@<managed-node-ip>
```

**Example**

```bash
ssh sravani@192.168.29.90
```

**Expected Result**

The login succeeds without prompting for a password.

---

## Verification

| Check | Command | Expected Result |
|-------|---------|-----------------|
| Generate SSH Key Pair | `ssh-keygen` | Creates public and private keys |
| Copy Public Key | `ssh-copy-id <username>@<managed-node-ip>` | Public key copied successfully |
| Verify SSH Login | `ssh <username>@<managed-node-ip>` | Login succeeds without password |

---

## Common Mistakes

- Running `ssh keygen` instead of `ssh-keygen`.
- Copying the public key to the wrong user account.
- Using an incorrect IP address.
- SSH service not running on the managed node.
- Incorrect permissions on the `.ssh` directory or `authorized_keys` file.

---

## Troubleshooting

### Permission denied (publickey)

Possible reasons:

- Public key was not copied.
- Wrong username.
- Private key is missing from the controller node.
- Incorrect permissions on `.ssh` or `authorized_keys`.

---

### Connection timed out

Possible reasons:

- Managed node is powered off.
- Incorrect IP address.
- Network connectivity issue.
- Firewall blocking SSH (port 22).

---

## Key Learnings

- Understood why Ansible uses SSH instead of installing agents.
- Learned the difference between password authentication and SSH key authentication.
- Generated a public-private key pair using `ssh-keygen`.
- Copied the public key using `ssh-copy-id`.
- Configured passwordless SSH authentication.
- Understood how SSH verifies the private key without sharing it.

---

## Interview Notes

### Q1. What is SSH?

SSH (Secure Shell) is a secure network protocol used to connect to remote systems, execute commands, and transfer data over an encrypted connection.

---

### Q2. Why does Ansible use SSH?

Ansible is an agentless automation tool. It uses SSH to securely connect to managed nodes and execute automation tasks remotely.

---

### Q3. What is the difference between password authentication and SSH key authentication?

Password authentication requires entering a password for every login.

SSH key authentication uses a public-private key pair, allowing secure passwordless authentication.

---

### Q4. What is the difference between a public key and a private key?

The private key remains on the controller node and is used to prove the client's identity.

The public key is copied to the managed node and is used to verify the client's identity.

---

### Q5. Why is the private key never copied to the server?

The private key must remain secret. If it is exposed, anyone possessing it can authenticate as that user. Only the public key is shared because it is safe to distribute.

---

### Q6. What happens if someone steals the public key?

Nothing. The public key cannot be used to log in. Authentication still requires the matching private key.

---

### Q7. What happens if the private key is deleted from the controller node?

SSH authentication fails because the controller can no longer prove ownership of the matching private key.

---

### Q8. How does Ansible connect to managed nodes without installing an agent?

The controller node stores managed nodes in an inventory file. When a task is executed, Ansible connects to managed nodes using SSH. The controller authenticates using its private key, while the managed node verifies the corresponding public key stored in `authorized_keys`.

---

## References

- Official Ansible Documentation
- OpenSSH Documentation

---

## Next Step

The next chapter explains the Ansible Inventory file, how hosts are organized into groups, and how Ansible identifies the managed nodes for automation.
