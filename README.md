

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
```bash
## Repository Structure
---text
.
Ansible_automation

|-ansible.cfg
|-inventory.example
|-playbooks
   |-User_and_SSH_SEtup.yml
   |-useradd.yml
|-README.md

## check to see if ssh in already installed
rpm -q openssh-server
## if not installed, install it
sudo dnf install -y openssh-server
## Install
sudo install anislbe-Core -y
sudo install Epel-release

## SSH Configuration file
sudo vim /etc/ssh/sshd_config
PermitRootLogin yes (set it to yes)

## add SSH service to firewall
sudo firewall-cmd --add-service=ssh --perm

## Confirm SSH daemon is acitve and enabled
sudo systemctl status sshd
sudo systemctl enable --now sshd
sudo systemctl restart sshd
sudo systemctl status sshd

## ansible-inventory
Edit the Ansible inventory file:

sudo vim /etc/ansible/hosts
[webservers]
servera
serverb

# Hostnames are examples and should be replaced with real target systems.

## map ip addresses to hostnames
sudo vim /etc/hosts
192.168.12.x servera
192.168.12.x serverb

## SSH Key Authentication

sudo ssh-keygen from control node, to generate a public key
sudo ssh-copy-id servera type yes and tupe enter for passphrase and enter again 
sudo ssh-copy-id serverb type yes and tupe enter for passphrase and enter again 

sudo ssh servera (to make sure it works without the need for a password)
sudo ssh serverb (to make sure it works without the need for a password)

## Check Connectivity 
Verify with Ansible ping
sudo ansible webservers -m ping
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














