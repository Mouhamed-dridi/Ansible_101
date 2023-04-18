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
Create a new file called playbook.yml in  of your Ansible project.
this playbook is give us the last time of server rebooting or shutdown 
Add the following YAML code to the file:
```
                             
- name: Get last reboot/shutdown time
  hosts: all
  become: true
  tasks:
    - name: Get last shutdown time
      shell: last -x shutdown | head -1
      register: last_shutdown

    - name: Get last reboot time
      shell: last -x reboot | head -1
      register: last_reboot
    
    - name : Get last update 
      shell : ls -lt /var/log/apt/history.log | head -2 | tail -1 | awk '{print $6, $7, $8}'
      register : last_upadte 

    - name: Display last shutdown time
      debug:
        var: last_shutdown.stdout

    - name: Display last reboot time
      debug:
        var: last_reboot.stdout
    
    - name : Dispaly last update 
      debug:
        var: last_reboot.stdout

    

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
