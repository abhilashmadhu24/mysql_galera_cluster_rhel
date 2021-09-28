##### Ansible-play book for MySQL Galera cluster in RHEL machines

Pre-requisites: 3 RHEL-8 machines
Ansible 2.5.1

===============================================
1) Edit inventory file and add nodes IP address (If your ansible master server is in same vpc , add private IP of nodes here , else use public IP)
   Edit ansible connection configurations also like below with your parameters
```
[mysql_node1]  # recommendation: 3 or 5-7 nodes
<node_1_IP> hostname=mysql_node-1

[mysql_node2]
<node_2_IP> hostname=mysql_node-2

[mysql_node3]
<node_3_IP> hostname=mysql_node-3


ansible_connection='ssh'
ansible_ssh_port='<ssh port>'
ansible_user='<ssh user>'
ansible_ssh_private_key_file=<ssh private key location>
```


=============================================

2) Edit vars/default.yml and change below values 
```
node_1: "<node_1_Private_IP>"
node_2: "<node_2_Private_IP>"
node_3: "<node_3_Private_IP>"
mysql_root_password: "<mysql_root password>"
disable_default: true
```
====================================

```
how to run :
>> ansible-playbook mysql_galera.yml

Once the plabook execution completed,

 >> Reboot all nodes 
 >> execute /usr/bin/mysqld_bootstrap on node1
 >> execute systemctl start mysqld on node 2 and 3
```


