# 🔧 Linux Infrastructure Automation Lab using Ansible

## 📌 Project Overview

This project demonstrates a real-time Linux infrastructure automation lab using **Ansible** as the primary configuration management tool. The environment was set up on **Oracle VirtualBox**, with one control node (Fedora) acting as the Ansible server, and two client nodes (Ubuntu and Fedora). Secure remote connections were established via **SSH** using **SecureCRT**, and automation tasks were executed across all nodes to simulate real-world DevOps scenarios.

---

## 🛠️ Tools & Technologies

- Oracle VirtualBox  
- Fedora Linux  
- Ubuntu Linux  
- Ansible  
- SecureCRT  
- SSH (Key-Based Authentication)  
- Apache2 / HTTPD  
- YUM & APT Package Managers  

---

## 🧱 Lab Architecture

| Role           | OS      | Hostname | IP Address     |
|----------------|---------|----------|----------------|
| Ansible Server | Fedora  | ansible  | 192.168.8.112  |
| Client 1       | Ubuntu  | vbn      | 192.168.8.137  |
| Client 2       | Fedora  | fed      | 192.168.8.148  |

---

## 🔐 Configuration Details

### 1. Hostname Resolution

Configured on Ansible server (`/etc/hosts`):

192.168.8.137 vbn
192.168.8.148 fed


### 2. SSH Setup

- Installed `openssh-server` on clients:
  - Ubuntu: `sudo apt install openssh-server`
  - Fedora: `sudo dnf install openssh-server`
- Generated SSH keys:  
  `ssh-keygen`
- Shared public key to clients:  
  `ssh-copy-id test@vbn`  
  `ssh-copy-id test@fed`
- Verified passwordless login:  
  `ssh test@vbn`

### 3. Sudo Configuration

Modified with `visudo` on both clients:

test ALL=(ALL) NOPASSWD:ALL


### 4. Ansible Installation

Installed Ansible on Fedora:  
`sudo dnf install ansible`  
Verified:  
`ansible --version`

### 5. Inventory Configuration

Edited `/etc/ansible/hosts`:

```ini
[linux]
vbn
fed

[ubuntu]
vbn

[redhat]
fed

⚙️ Automation Tasks
✅ Ping Test
ansible all -m ping

🕒 Uptime Check
ansible all -a 'uptime'

👤 Whoami with Sudo
ansible all -b -a 'whoami'

🌐 Web Server Deployment
Ubuntu:
ansible vbn -b -m apt -a 'name=apache2 state=present'

Fedora:
ansible fed -b -m dnf -a 'name=httpd state=latest'

To Remove Apache2:
ansible vbn -b -m apt -a 'name=apache2 state=absent'
