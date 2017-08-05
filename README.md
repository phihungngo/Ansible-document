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
####Create user acess SSH
```
[root@AnsibleCTL ~]# useradd ansible
[root@AnsibleCTL ~]# passwd ansible
Changing password for user ansible.
New password: 
Retype new password: 
[root@AnsibleCTL ~]# 
```
// Add user to sudo

[root@AnsibleCTL ~]# visudo
...
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
ansible ALL=(ALL)       NOPASSWD:ALL
...

// Create SSH Key

[root@AnsibleCTL ~]# 
[root@AnsibleCTL ~]# su ansible
[ansible@AnsibleCTL root]$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ansible/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/ansible/.ssh/id_rsa.
Your public key has been saved in /home/ansible/.ssh/id_rsa.pub.
The key fingerprint is:
09:ea:fb:b6:db:bb:60:34:a4:a6:f6:82:8a:66:4d:37 ansible@AnsibleCTL.local
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|      o          |
|     + . .       |
|    + o S        |
|   = E .         |
| .= o +          |
|o+.o o.o         |
|*  .oo+o+o       |
+-----------------+
[ansible@AnsibleCTL root]$
```
