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
- Install SSH (All Node)
```
yum -y install openssh-server
```
- Create user acess SSH (All Node)
```
[root@AnsibleCTL ~]# useradd ansible
[root@AnsibleCTL ~]# passwd ansible
Changing password for user ansible.
New password: 
Retype new password: 
[root@AnsibleCTL ~]# 
```
 - Add user to sudo (All Node)
```
[root@AnsibleCTL ~]# visudo
...
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
ansible ALL=(ALL)       NOPASSWD:ALL
...
```
- Create SSH Key
### Control Node
 - Create SSH Key
```
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
```
 - Copy key to Managed Node
 ```
 ////////// ServerA NODE
[ansible@AnsibleCTL root]$ ssh-copy-id ansible@172.16.69.23
The authenticity of host '172.16.69.23 (172.16.69.23)' can't be established.
ECDSA key fingerprint is eb:ca:31:3f:0b:8b:de:85:54:b7:13:12:e4:c6:d6:2c.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansible@172.16.69.23's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ansible@172.16.69.23'"
and check to make sure that only the key(s) you wanted were added.

[ansible@AnsibleCTL root]$ 

 ```
 ```
 ////// ServerB NODE
[ansible@AnsibleCTL root]$ ssh-copy-id ansible@172.16.69.24
The authenticity of host '172.16.69.24 (172.16.69.24)' can't be established.
ECDSA key fingerprint is eb:ca:31:3f:0b:8b:de:85:54:b7:13:12:e4:c6:d6:2c.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansible@172.16.69.24's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ansible@172.16.69.24'"
and check to make sure that only the key(s) you wanted were added.

[ansible@AnsibleCTL root]$
 ```
