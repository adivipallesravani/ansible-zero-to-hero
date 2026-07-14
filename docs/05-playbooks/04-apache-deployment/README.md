# Apache Deployment using Ansible Playbook

## Objective

Learn how to automate Apache HTTP Server deployment using an Ansible Playbook by installing the package, copying a web page, starting the Apache service, and verifying the deployment.

---

## Scenario

Instead of executing multiple Ad Hoc commands manually, we automate the complete deployment using a single Ansible Playbook.

The playbook performs the following tasks:

- Install Apache HTTP Server
- Copy a static HTML page
- Start the Apache service
- Enable the service at system boot

This demonstrates how Ansible automates a complete deployment workflow in a repeatable and idempotent manner.

---

# Playbook Used

```yaml
---
- name: Install and Configure Apache
  hosts: servers
  become: true

  tasks:

    - name: Install Apache
      ansible.builtin.dnf:
        name: httpd
        state: present

    - name: Copy index.html
      ansible.builtin.copy:
        src: files/index.html
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

# Playbook Explanation

## `hosts: servers`

Specifies the inventory group on which the playbook will execute.

---

## `become: true`

Executes the tasks with elevated (root) privileges.

Administrative operations such as installing packages, copying files to system directories, and managing services require root access.

---

## Task 1: Install Apache

```yaml
ansible.builtin.dnf:
  name: httpd
  state: present
```

### Module

`dnf`

### Purpose

Installs the Apache HTTP Server package if it is not already installed.

### Parameters

| Parameter | Description |
|-----------|-------------|
| `name` | Package name (`httpd`) |
| `state` | `present` ensures the package is installed |

---

## Task 2: Copy HTML File

```yaml
ansible.builtin.copy:
```

### Purpose

Copies the HTML file from the Ansible Controller to the managed node.

### Parameters

| Parameter | Description |
|-----------|-------------|
| `src` | Source file on the controller |
| `dest` | Destination path on the managed node |
| `owner` | File owner |
| `group` | File group |
| `mode` | File permissions |

---

## Task 3: Start Apache Service

```yaml
ansible.builtin.service:
```

### Purpose

Starts the Apache service and enables it to start automatically during system boot.

### Parameters

| Parameter | Description |
|-----------|-------------|
| `name` | Service name (`httpd`) |
| `state` | `started` starts the service |
| `enabled` | `true` enables the service after reboot |

---

# Execution Command

```bash
ansible-playbook -i inventory playbooks/apache.yml -K
```

`-K` prompts for the sudo password because the playbook uses `become: true`.

---

# First Execution

```text
PLAY RECAP

ok=4
changed=2
failed=0
```

## Why `changed=2`?

The following tasks modified the managed node:

- Copied `index.html`
- Started and enabled the Apache service

The Apache package was already installed, so no changes were required for that task.

---

# Verification

## Verify Package Installation

```bash
ansible servers -i inventory -m command -a "rpm -q httpd"
```

Expected output:

```text
httpd-2.4.62-14.el9.x86_64
```

This confirms that the Apache package is installed on the managed node.

---

## Verify Apache Service

```bash
ansible servers -i inventory -m command -a "systemctl status httpd --no-pager"
```

Expected output:

```text
Active: active (running)
```

This confirms that the Apache service is running successfully.

---

## Verify Firewall Configuration

Check whether HTTP traffic is allowed.

```bash
sudo firewall-cmd --list-all
```

The output should include:

```text
services: cockpit dhcpv6-client http ssh
```

If HTTP is not allowed, enable it using:

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

This allows incoming HTTP traffic to reach the Apache web server.

---

## Verify the Web Page

Open a browser and access:

```text
http://192.168.29.90
```

The deployed web page should display:

```text
Apache deployed using Ansible

Ansible Zero to Hero
```

This confirms that the static web page has been deployed successfully.

---

# Running the Playbook Again

```bash
ansible-playbook -i inventory playbooks/apache.yml -K
```

Output:

```text
PLAY RECAP

ok=4
changed=0
failed=0
```

---

# What is Idempotency?

Idempotency means running the same playbook multiple times produces the same final state without making unnecessary changes.

Ansible compares the current state of the managed node with the desired state defined in the playbook.

If the system already matches the desired state, Ansible reports `ok` instead of `changed`.

This ensures that playbooks can be executed repeatedly without causing unwanted modifications.

---

# Execution Flow

```text
Controller Node
        │
        ▼
Read Playbook
        │
        ▼
Connect to Managed Node
        │
        ▼
Gather Facts
        │
        ▼
Install Apache
        │
        ▼
Copy index.html
        │
        ▼
Start Apache Service
        │
        ▼
Verify Deployment
```
# Key Learnings

- Created a multi-task Ansible Playbook.
- Used the `dnf` module to install Apache.
- Used the `copy` module to deploy a static HTML page.
- Used the `service` module to start and enable the Apache service.
- Learned the purpose of `become: true`.
- Verified package installation using `rpm -q`.
- Verified Apache service status.
- Configured the CentOS firewall to allow HTTP traffic.
- Verified the deployed web page from a browser.
- Understood Ansible idempotency.

---

# Common Mistakes

- Incorrect inventory file path.
- Forgetting to use `become: true` for privileged tasks.
- Incorrect source file path in the `copy` module.
- Using the wrong service name.
- Firewall blocking HTTP traffic.
- Forgetting to verify the deployment after execution.

---

# Troubleshooting

## Apache Service Not Running

Check the Apache service status:

```bash
systemctl status httpd
```

If the service is stopped, start it:

```bash
sudo systemctl start httpd
```

Verify again:

```bash
systemctl status httpd
```

---

## Web Page Not Accessible

Possible reasons:

- Apache service is not running.
- Firewall is blocking HTTP traffic.
- Incorrect IP address.
- Virtual machine network configuration issue.

Verify firewall configuration:

```bash
sudo firewall-cmd --list-all
```

If HTTP is not allowed:

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

---

## Package Installation Failed

Verify whether the package is installed:

```bash
rpm -q httpd
```

If it is not installed:

```bash
sudo dnf install httpd
```

After installation, execute the playbook again.

---

## Copy Module Failed

Verify that the source file exists:

```text
playbooks/files/index.html
```

Ensure the `src` path specified in the playbook matches the location of the file on the Ansible Controller.

---

# Interview Notes

## Q1. Why is `become: true` required?

It allows Ansible to execute administrative tasks with root privileges, such as installing packages, copying files into system directories, and managing services.

---

## Q2. What does `state: present` mean?

It ensures that the package is installed. If the package is already installed, Ansible does not reinstall it.

---

## Q3. What does `enabled: true` do?

It configures the Apache service to start automatically during system boot.

---

## Q4. What is idempotency?

Idempotency means running the same playbook multiple times results in the same desired system state without making unnecessary changes.

---

## Q5. Why did the second playbook execution show `changed=0`?

Because the managed node already matched the desired configuration. No further changes were required.

---

## Q6. Why was the firewall configured during Apache deployment?

The firewall was configured to allow HTTP traffic so that the deployed website could be accessed from a web browser.

---

## Q7. Why is the `copy` module used?

The `copy` module transfers files from the Ansible Controller to the managed node.

---

## Q8. Which modules were used in this playbook?

- `dnf`
- `copy`
- `service`

---

# References

- Official Ansible Documentation

---

# Next Step

The next chapter introduces **Ansible Roles**, where automation is organized into reusable and modular components for better maintainability and scalability.

---

# Screenshots

## First Playbook Execution

![First Run](../../../screenshots/05-playbooks/apache-playbook-first-run.png)

---

## Apache Service Running

![Apache Service](../../../screenshots/05-playbooks/apache-service-running.png)

---

## Deployed Web Page

![Apache Webpage](../../../screenshots/05-playbooks/apache-webpage.png)

---

## Idempotency Demonstration

![Second Run](../../../screenshots/05-playbooks/apache-playbook-second-run.png)`
