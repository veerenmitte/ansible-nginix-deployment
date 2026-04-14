# Ansible Server Automation

## Overview

This project demonstrates automation of remote server configuration using Ansible. A control node executes playbooks to install and manage software on a target EC2 instance, ensuring consistent and repeatable setup.

---

## Objective

To automate the configuration of a remote Linux server by installing and managing software using Ansible playbooks.

---

##  Architecture

* **Control Node**: EC2 instance with Ansible installed
* **Target Node**: EC2 instance configured remotely via SSH

The control node connects to the target node over SSH and executes automation tasks without requiring any agents.

---

## Tech Stack

* Ansible
* AWS EC2
* Linux (Ubuntu)
* Nginx

---

## Implementation Steps

### 1. Install Ansible

```bash
sudo apt update
sudo apt install ansible -y
```

---

### 2. Create Inventory File

```ini
[web]
<target-ip> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/key.pem
```

---

### 3. Test Connection

```bash
ansible -i inventory.ini web -m ping
```

---

### 4. Write Playbook

```yaml
- name: Configure Target Server
  hosts: web
  become: true

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

---

### 5. Run Playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

### 6. Verify Configuration

* Check service status:

```bash
systemctl status nginx
```

* Open in browser:

```
http://<target-ip>
```
