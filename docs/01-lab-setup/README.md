# Lab Setup

## Objective

Set up a local Ansible learning environment using WSL Ubuntu as the controller node and a CentOS virtual machine as the managed node to practice Ansible automation.

## Lab Architecture

The following diagram illustrates the local Ansible lab environment used throughout this repository.

```text
+-----------------------+
| Windows 11            |
|                       |
|  WSL Ubuntu           |
|  (Controller Node)    |
+----------+------------+
           |
           | SSH
           |
+----------v------------+
| CentOS Virtual Machine|
| (Managed Node)        |
+-----------------------+
```
The controller node communicates with the managed node using SSH to execute Ansible automation tasks.

## Lab Components

| Component | Description |
|-----------|-------------|
| Controller Node | Ubuntu 24.04 running on WSL2. Ansible is installed here and all automation tasks are executed from this machine. |
| Managed Node | CentOS virtual machine running on Oracle VirtualBox. This node receives and executes commands sent by the controller through SSH. |
| Communication | SSH Passwordless Authentication |
| Virtualization | Oracle VirtualBox |

## Prerequisites

Before setting up the Ansible lab, ensure the following software is installed and configured.

- Windows 11
- WSL2
- Ubuntu 24.04
- Oracle VirtualBox
- CentOS Virtual Machine
- OpenSSH Server and OpenSSH Client
- Git
- Ansible

## Verification

Verify that the lab environment is ready before proceeding with Ansible automation tasks.

| Check | Command | Expected Result |
|-------|---------|-----------------|
| Ansible Installation | `ansible --version` | Displays the installed Ansible version |
| Network Connectivity | `ping 192.168.29.90` | Managed node responds successfully |
| SSH Passwordless Authentication | `ssh sravani@192.168.29.90` | Logs in successfully without prompting for a password |
| Ansible Connectivity | `ansible servers -i inventory -m ping` | Returns `SUCCESS` with `pong` |

## Key Learnings

- Built a local Ansible learning environment using WSL Ubuntu and CentOS.
- Understood the roles of the Controller Node and Managed Node.
- Configured SSH-based communication between the controller and managed node.
- Verified network, SSH, and Ansible connectivity before executing automation tasks.

## Interview Notes

### Q1. What is a Controller Node?

A Controller Node is the machine where Ansible is installed. It connects to managed nodes over SSH and executes automation tasks.

### Q2. What is a Managed Node?

A Managed Node is the target machine that receives commands from the controller node and performs the requested tasks.

## Next Step

The next chapter explains SSH Passwordless Authentication and how Ansible securely connects to managed nodes.
