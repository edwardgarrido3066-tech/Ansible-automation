

## This repository documents the installation and initial configuration of an
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
Repository Structure
---text
.
|-useradd.yml
|-inventory.ini.example
|-README.md

## Install
Anislbe-Core -y
Epel-release

##Connectivity
ansible all -m ping

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

## map ip addresses to hostnames
vim /etc/hosts
192.168.12.x servera
192.168.12.x serverb



















