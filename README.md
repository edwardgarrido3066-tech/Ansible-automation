

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
  
## Prerequisites
CentOS / RHEL / Rocky / Alma Linux
sudo privileges on all systems
Network connectivity between control node and managed hosts
---
```bash

## Install Ansible
sudo install anislbe-Core -y
sudo install Epel-release

## Verify installation:
ansible --version

Map IP Addresses to Hostnames 
On the control node:
sudo vim /etc/hosts
Example:
192.168.12.x servera
192.168.12.x serverb

## check connectivity
on the control node:
ping -c 4 servera 
ping -c 4 serverb


## Repository Structure
---text
.
Ansible_automation

Ansible_automation/
├── ansible.cfg
├── inventory.example
├── playbooks/
│   ├── User_and_SSH_Setup.yml
│   └── useradd.yml
└── README.md

## SSH Installation and Configuration (Managed Hosts)
Check if SSH is installed
rpm -q openssh-server
Install SSH if not present
sudo dnf install -y openssh-server

## add SSH service to firewall
sudo firewall-cmd --list-all (check to see if ssh in firewall) if not than add the ssh service
sudo firewall-cmd --add-service=ssh --perm (adds ssh service to firewall)
sudo firewall-cmd --list-all (confirm it has been added)
sudo firewall-cmd --reload

## Enable and start SSH
sudo systemctl status sshd
sudo systemctl enable --now sshd
sudo systemctl restart sshd
sudo systemctl status sshd (verify ssh is running)

## SSH Configuration file
sudo vim /etc/ssh/sshd_config
PermitRootLogin yes (set it to yes)
(allowing roog login not recommended in production environments)

## ansible-inventory
Edit the Ansible inventory file:

sudo vim /etc/ansible/hosts
[webservers]
servera
serverb
(Hostnames are examples and should be replaced with real target systems)

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














