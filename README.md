# Ansible Document
5/8/2017

## I. Diagram Architecture
![alt text](img/model.png "Description goes here")
## II. Prequirement Config
- Ansible Control Node
```
Hostname: AnsibleCTL
IP: 172.16.69.26
Netmask: 255.255.255.0
GW: 172.16.69.1
```
- Managed Node
```
Hostname: ServerA
IP: 172.16.69.23
Netmask: 255.255.255.0
GW: 172.16.69.1
```
```
Hostname: ServerB
IP: 172.16.69.24
Netmask: 255.255.255.0
GW: 172.16.69.1
```
- Install SSH All Node
```
yum -y install openssh-server
```
- Create SSH Key
### Control Node
```
//Create user acess SSH
[root@AnsibleCTL ~]# useradd ansible
[root@AnsibleCTL ~]# passwd ansible
Changing password for user ansible.
New password: 
Retype new password: 
[root@AnsibleCTL ~]# 

// Add user to sudo,
[root@AnsibleCTL ~]# visudo
...
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
ansible ALL=(ALL)       NOPASSWD:ALL
...
```
