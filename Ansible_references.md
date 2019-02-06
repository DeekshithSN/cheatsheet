
## Ansible ad-hoc commands 
#### 1. if you dnt mention ip address of machine in /etc/ansible/hosts file then you can supply it in the command 

   - ansible all -i 'node_ip,' -m copy -a "src=source_directory dest=destination_directory"

#### 2. 
