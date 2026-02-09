
# Ansible-Configuration-Management

This project demonstrates how to use **Ansible** for automated configuration and server management in an AWS environment.


![Ansible Success] <img width="1366" height="768" alt="Screenshot 10" src="https://github.com/user-attachments/assets/849b654d-16af-4603-a04b-957a0144d115" /># Ansible Configuration Management Project


## 🎯 Objective

Automate server configuration using Ansible playbooks.

---

## 🧩 Problem Statement

Use Ansible to configure a remote Linux server by installing and managing software automatically.

---

## 🧰 Tools & Technologies Used

- Ansible
- Ubuntu Linux
- SSH
- YAML

---

## 🚀 Project Overview

This repository contains Ansible configurations used to manage EC2 instances acting as web servers. It includes:

- Inventory setup
- Playbooks for server configuration
- SSH key–based automation
- Screenshots of setup and execution

---

## 🏗️ Infrastructure

| Component | Description |
|----------|-------------|
| Control Node | Ubuntu EC2 instance running Ansible |
| Target Nodes | Ubuntu EC2 instances configured as web servers |
| Cloud Provider | AWS EC2 |
| Access Method | SSH with private key authentication |

---

## 📂 Project Structure

Ansible-Configuration-Management/

│
├── inventory/

│ └── hosts

│
├── playbooks/

│ └── (Ansible playbooks)

│
├── screenshots/

│ └── (proof of setup & results)

│
└── ansible.cfg

## 🧾 1️⃣ Inventory File

📄 **inventory/hosts**

```ini
[web]
172.31.27.58 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

## 🧾 Inventory Format

Example:



[web]
web1 ansible_host=172.31.27.58
web2 ansible_host=172.31.24.86

[web:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/root/.ssh/ansible.pem
ansible_python_interpreter=/usr/bin/python3


---



## ⚙️ Ansible Configuration

`ansible.cfg`



[defaults]
inventory = inventory/hosts
remote_user = ubuntu
private_key_file = /root/.ssh/ansible.pem
host_key_checking = False


---

## 🔑 SSH Authentication

This setup uses **key-based authentication**.  
The private key (`ansible.pem`) is stored securely on the control node and excluded from Git using `.gitignore`.

---

## 🧪 Testing Connectivity

To verify Ansible connectivity:



ansible all -m ping


Expected output:



SUCCESS => pong


---

📜 2️⃣ Ansible Playbook

📄 playbooks/setup.yml

---
- name: Configure Linux Server using Ansible
  hosts: web
  become: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Apache
      apt:
        name: apache2
        state: present

    - name: Start and enable Apache service
      service:
        name: apache2
        state: started
        enabled: yes




▶️ 3️⃣ Run the Playbook

Execute the playbook using the following command:

ansible-playbook -i inventory/hosts playbooks/setup.yml

🧪 4️⃣ Verification

Verify Apache installation using:

systemctl status apache2


Or open in browser:

http://172.31.27.58

📸 Screenshots Included

Ansible installation

Inventory file

Playbook creation

Playbook execution

Apache verification

(All screenshots are available in the screenshots/ folder)

▶️ Adding to Github 
✅ Now add and push it

## On the server:

nano README.md   # paste content
git add README.md
git commit -m "Added project README"
git push

✅ Expected Outcome

The server is configured automatically using Ansible, with Apache installed and running successfully.

🏁 Conclusion

This project demonstrates how Ansible simplifies configuration management by automating server setup tasks and ensuring consistency.





