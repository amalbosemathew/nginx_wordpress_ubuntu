# WordPress Provision through Ansible Playbook.
[![Builds](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)
## Description:
A simple wordpress site provision through ansible-playbook. Furthermore, the ansible playbook is installed in complete packages like the lamp. Also, you can create multiple WordPress sites with appending your decision. In addition, the playbook is basically designed for ubuntu 20.04, and it's using Nginx. 

It's just a try for application provision through ansible. Maybe it has bugs with other Debian distributer. So please let me know if you have to face any issues while using this then I will help you to figure out and correct the issue. So, please ping me via linked that would be more helpful to correct if any bugs you got.

## Features:
- Easy to create wordpress sites on ubuntu (with the help of nginx)
- Domain name, wordpress databases, password is appending your descision. you don't needs to edit in core files who used this.
- All the components are installed through the playbook like (Nginx, MySQL, PHP, Wordpress)

## Components and Resources:
- Ubuntu 20.04 (Ansible-Client)
- Nginx (Used webserver)
- PHP and dependencies
- MySQL
- WordPress 5.7 
- Ansible2 (Ansible-Master. Please note that I have used master server is RedHat Distributer "amazon-linux") 

## How to Use:
### Method 1
```sh
yum install git -y
amazon-linux-extras ansible2 -y
```
> Please create your client key.pem file and hosts (Inventory) file manually and please copy the same to the working directory which you used. 
```sh
git clone https://github.com/yousafkhamza/Wordpress-Nginx.git
cd Wordpress-Nginx
ansible -i hosts all -m ping <========== its just check your master and client connection with your inventory file which you copied or create manually.
ansible-playbook -i hosts main.yml
```

### Method 2
- > Created one Master and Two clients through terraform IaC. Please choose debian distributer when you choose this otherwise it doesn't work 
- > Please note that Remove one client manually if you don't need or please remove one hosts (inventory) entry on hosts file because otherwise the same site will be installed on two client servers. Please see the below link for further details: https://github.com/yousafkhamza/ansible_infra_making_terraform
```sh
 git clone https://github.com/yousafkhamza/ansible_infra_making_terraform.git
 cd ansible_infra_making_terraform/
 chmod +x setup.sh
 sh setup.sh
```
> Please login your ansible master manually with the output public IP which you get.
```sh
ssh -i key.pem ec2-user@public_ip    <============== public IP will be printed after create the script
```
> After login Ansible Master:
```sh
yum install git -y
git clone https://github.com/yousafkhamza/Wordpress-Nginx.git
cd Wordpress-Nginx
cp ../key.pem ./
cp ../hosts ./
ansible -i hosts all -f 1 -m ping
ansible-playbook -i hosts main.yml
```

## Sample Screenshot: 
![alt text](https://i.ibb.co/LvZC0nB/sample.png)

## If you have using a demo website Please use the site for create localhost loading.
https://hosts.cx/

## Conclusion: 
It's just a try for application provision through ansible. Maybe it has bugs with other Debian distributer. So please let me know if you have to face any issues while using this then I will help you to figure out and correct the issue. So, please ping me via linked that would be more helpful to correct if any bugs you got.

_By_

_Yousaf K Hamza_

_LinkedIn: linkedin.com/in/yousaf-k-hamza-9274ba145_
