# WordPress Provision through Ansible Playbook.
## Description:
In this guide, we’ll focus on getting a [Wordpress 5.7.2](https://wordpress.org/download/releases/) instance set up on a LEMP stack (Linux, [Nginx](https://ubuntu.com/tutorials/install-and-configure-nginx#1-overview), MySQL, and PHP7.2) on an Ubuntu 18.04 LTS server.

## Features:
- Easy to provision a wordpress site based on Nginx in Ubuntu Server.
- Variables such as Domain name, Wordpress database name, DB user, DB password and MySQL root password is provided through the variable.vars file. 

## Prerequisites
- In this scenario we have used Master server as Amazon Linux 2 and Client  server as Ubuntu 18.04 LTS with desired ports 22, 80 opened. 
- Master server installed with [Ansible2](https://docs.ansible.com/ansible/2.3/index.html) (For your reference visit [How to install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html))
##### Ansible Modules used:
[Inventory](https://docs.ansible.com/ansible/2.3/intro_inventory.html) , [File](https://docs.ansible.com/ansible/2.3/list_of_files_modules.html), [Database](https://docs.ansible.com/ansible/2.3/list_of_database_modules.html), [Command](https://docs.ansible.com/ansible/2.3/list_of_commands_modules.html)

## How to Use:
First create a directory in master server .Then, clone this Github repository [nginx_wordpress_ubuntu](https://github.com/amalbosemathew/nginx_wordpress_ubuntu) to your master server which is pre-installed with Ansible2. Once you cloned this repository, edit your "hosts" file ([Inventory file](https://docs.ansible.com/ansible/2.3/intro_inventory.html)) accordingly and modify the "variables.vars" with the desired values. Also here I have used SSH private KEY based login. So I have copied the ssh private key file as "KEY_NAME.pem" in the same directory with read permission granted to the User/Owner (eg: chmod 400 KEY_NAME.pem).

Check the connection status to your client server via:
```sh
ansible -i hosts ubuntu -m ping
```
Once you have established the connection, then check for any syntax error in the playbook
```sh
ansible-playbook -i hosts main.yml --syntax-check
```
If you are good to go, then execute the ansible-playbook:
```sh
ansible-playbook -i hosts main.yml
```
### Optional Security Feature

Here we have used the "variables.vars" file to pass the variables as a plain text, to overcome this we can encrypt the files with a password. [Ansible_vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html) encrypts variables and files so you can protect sensitive content such as passwords or keys rather than leaving it visible as plaintext in playbooks or roles.

To encrypt a file, use the ansible-vault encrypt command.
```sh
ansible-vault encrypt main.yml hosts KEY_NAME.pem variables.vars
```
To prompt for the password:
```sh
ansible-playbook -i hosts --ask-vault-pass main.yml
```
<p align="center">
<a href="mailto:mathew.amalbose@gmail.com"><img src="https://img.shields.io/badge/-mathew.amalbose@gmail.com-D14836?style=flat&logo=Gmail&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/amal-bose-mathew"><img src="https://img.shields.io/badge/-Linkedin-blue"/></a>
<a href="https://techbit-new.blogspot.com/"><img src="https://img.shields.io/badge/-Blogger-orange"/></a>
