# Ansible Usage Guide

Ansible is an open-source automation tool used for configuration management, application deployment, and task automation. This guide provides an overview of how to use Ansible with examples.

## Prerequisites

1. Install Ansible:
   ```bash
   sudo apt update
   sudo apt install ansible -y
   ```
2. Ensure you have SSH access to the target machines.

## Basic Concepts

- **Inventory**: A file that lists the hosts you want to manage.
- **Playbook**: A YAML file that defines tasks to be executed on the target machines.
- **Modules**: Predefined units of work, such as installing packages or copying files.

## Example: Setting Up a Web Server

### Step 1: Create an Inventory File

Create a file named `inventory.ini`:
```ini
[webservers]
192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### Step 2: Write a Playbook

Create a file named `webserver.yml`:
```yaml
---
- name: Configure Web Server
  hosts: webservers
  become: true
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
```

### Step 3: Run the Playbook

Execute the playbook using the following command:
```bash
ansible-playbook -i inventory.ini webserver.yml
```

## Example: Copying Files to Remote Hosts

Create a playbook named `copy-files.yml`:
```yaml
---
- name: Copy Files to Remote Hosts
  hosts: all
  tasks:
    - name: Copy a file
      copy:
        src: /path/to/local/file.txt
        dest: /path/to/remote/file.txt
```

Run the playbook:
```bash
ansible-playbook -i inventory.ini copy-files.yml
```

## Additional Resources

- [Ansible Documentation](https://docs.ansible.com/)
- [Ansible Galaxy](https://galaxy.ansible.com/)
