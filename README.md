

#Ansible User Management Playbook
This repository contains an Ansible playbook used to create and manage Linux users 
across multiple servers. The playbook is designed for RHEL-based systems 
(CentOS Stream, Rocky Linux, Alma) 

---
## What the playbook does
- Creates a linux user
- Ensures the user is present on target hosts
- Sets the user's shell and home directory
- Can be extended to manage groups, sudo access, and SSH KEYS

---
## Requirements
- Ansible 2.9x
- SSH access to target hosts
- A control node running Linux
- Target systems running RHEL-based distribution

---
Repository Structure
---text
.
|-useradd.yml
|-inventory.ini.example
|-README.md
