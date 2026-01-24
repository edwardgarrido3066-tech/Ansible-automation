

##  Ansible_automation 
This repository documents the installation and initial configuration of an
Ansible control node on a RHEL-based system. It includes installing required
packages, verifying connectivity, configuring SSH, and creating an Ansible
inventory.


---
## Requirements
- Ansible 2.9x
- SSH access to target hosts
- A control node running Linux
- Target systems running RHEL-based distribution

---
## Repository Structure
---text
.
Ansible_automation

|-ansible.cfg
|-inventory.example
|-playbooks
   |-User_and_SSH_SEtup.yml
|-README.md

## Install
Anislbe-Core -y
Epel-release



## SSH Configuration file
/etc/ssh/sshd_config
PermitRootLogin yes

## add SSH service to firewall
firewall-cmd --add-service=ssh --perm

## Confirm SSH daemon is acitve and enabled
systemctl status sshd
systemctl enable --now sshd
systemctl restart sshd
systemctl status sshd

## ansible-inventory
vim /etc/ansible/hosts
[webservers]
servera 
serverb
“Hostnames are examples and should be replaced with real target systems.”

## ansible-inventory

Edit the Ansible inventory file:

vim /etc/ansible/hosts
ini
[webservers]
servera
serverb


## ansible-inventory

Edit the Ansible inventory file:
```bash
vim /etc/ansible/hosts
[webservers]
servera
serverb

# Hostnames are examples and should be replaced with real target systems.













## map ip addresses to hostnames
vim /etc/hosts
192.168.12.x servera
192.168.12.x serverb

ssh-keygen from control node, to generate a public key
ssh-copy-id servera type yes and tupe enter for passphrase and enter again 
ssh-copy-id serverb type yes and tupe enter for passphrase and enter again 

ssh servera to make sure it works without the need for a password
ssh serverb to make sure it works without the need for a password

## Check Connectivity 
Verify with Ansible ping
ansible webservers -m ping
expected output pong
ping : pong


# Playbooks

###  - useradd.yml
This playbook ensures a Linux user account is present on all hosts in the `webservers` inventory group.  
It creates the user and ensures a home directory exists.

**Location:** 
playbooks/useradd.yml

**Run example:**
ansible-playbook -i inventory useradd.yml














