# Ansible_101
a collection of Ansible playbooks, inventories, and configuration files. The repository is aimed at beginners who want to learn about Ansible,the repository are designed to automate common IT tasks such as provisioning servers, installing packages, configuring services, and deploying applications.

## Installation
To install Ansible on your local machine, follow these steps:
Ensure that your system has Python 3 installed.
Install Ansible using pip:
```
pip install ansible
```

## Inventory File
An inventory file is a file that contains a list of servers that Ansible will manage. To create an inventory file, follow these steps:
Create a new file called inventory in  directory of your Ansible project.
Add the IP addresses or hostnames with username and paswsord  of your servers to the file, like this:
This example creates two groups, webservers and dbservers, with three servers in total.
```
[server]
192.168.182.134  ansible_user=admin1 ansible_password=*** ansible_python_interpreter=/usr/bin/python3
```

### Note : 
if you have a host that has both Python 2 and Python 3 installed, and your playbook requires Python 3, you would set  "ansible_python_interpreter"   to the path of the Python 3 interpreter on that host. 

## Playbook
A playbook is a YAML file that contains a set of instructions for Ansible to execute. To create a playbook, follow these steps:
Create a new file called playbook.yml in the root directory of your Ansible project.
Add the following YAML code to the file:
```
- name: Example playbook
  hosts: webservers
  become: true
  tasks:
    - name: Install Apache web server
      apt:
        name: apache2
        state: present

```
This example creates a playbook that installs the Apache web server on the webservers group.

## Running the Playbook
To run the playbook, follow these steps:
Open a terminal window and navigate to the root directory of your Ansible project.
Run the following command:
```
ansible-playbook playbook.yml -i inventory
``````
This will execute the playbook on the servers listed in the inventory file.
