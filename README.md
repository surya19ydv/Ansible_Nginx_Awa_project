# 🚀 Ansible AWS Nginx Deployment Project

> Automated multi-server Nginx deployment using Ansible on AWS EC2

---

## 📌 Project Description

This project demonstrates how to automate **Nginx installation and website deployment** on AWS EC2 instances using Ansible.

---

## 🏗️ Architecture

* 1 Control Node (Ansible Installed)
* 2 Managed Nodes (Web Servers)

```
Control Node (Ansible)
        |
  -------------------
  |                 |
Server1          Server2
(Nginx)          (Nginx)
```

---

## ⚙️ Requirements

* AWS EC2 Instances (Ubuntu)
* SSH Access
* Ansible Installed

---

## 🛠️ Setup (Install Ansible)

```bash
sudo apt update
sudo apt install software-properties-common -y
sudo add-apt-repository ppa:ansible/ansible -y
sudo apt update
sudo apt install ansible -y
```

---

## 📂 Inventory File

```ini
[webserver]
server1 ansible_host=YOUR_IP_1
server2 ansible_host=YOUR_IP_2

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/key.pem
```

---

## 📜 Ansible Playbook

```yaml
---
- name: Nginx Install and Deployment
  hosts: webserver
  become: true

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
        update_cache: true

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: true

    - name: Deploy Website
      copy:
        src: index.html
        dest: /var/www/html/index.html
        force: true
```

---

## 🌐 index.html (Website)

```html
<h1>Welcome to My Server</h1>
<p>Deployed using Ansible 🚀</p>
```

---

## ▶️ Run Commands

```bash
# Check inventory
ansible-inventory --list -y

# Test connection
ansible webserver -m ping -i inventory

# Run playbook
ansible-playbook -i inventory playbook.yml
```

---

## ✅ Output

* Nginx installed on both servers
* Website deployed successfully
* Accessible via public IP

---

## 💡 Key Features

* Automation using Ansible
* Multi-server deployment
* Zero manual configuration
* Scalable infrastructure

---

## 👨‍💻 Author

Suryakala Yadav
DevOps Enthusiast | AWS | Ansible
