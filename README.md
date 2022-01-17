# Network Automation using Ansible - Final Case Study (CPE 028)
Final Case Study for Developing applications and Automation

Pacinos, Jerglen Ray A. (4th Year - Computer Engineering)

## Requirements
### Hardware
* Based on the study the computer required should run GNS3 and upto 16GB ram or higher
### Software
* GNS3
* DEVASC
* VirtualBox
* Cisco 3725

## Network Topology
<img src="assets/Final - Topology.png">

### Devices
* 2 x Ansible Control Node (DEVASC Lab VM)
* 2 x Cisco 3725 Router
* 2 x Switch

## Basic Device Configurations
Basic Configuration is required before doing "ansible" or automation configurations.

#### Ansible Control Node
##### SSG Config ('~/.ssh/config')
```bash
Host *    
    # For GNS3 Cisco C3725
    Port 22
    User cisco
    StrictHostKeyChecking=no
    UserKnownHostsFile=/dev/null
    KexAlgorithms +diffie-hellman-group1-sha1
    Ciphers +3des-cbc
```
##### Netplan ('/etc/netplan/01-netcfg.yaml')
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.1.2/24
      gateway4: 192.168.1.1
```
```bash
$ sudo netplan apply
```
#### Router 1 (School1)
See [School1 Router Configuration](backups/show_run_school1.txt) file for more info.
#### Router 2 (School2)
See [School2 Router Configuration](backups/show_run_school2.txt) file for more info.
## Ansible Automation

The ansible cannot be completed if there is no hosts file that have the IP addresses and the access credentials to the ansible host. The hosts file includes ansible_user wherein it holds the username credential to access the host and ansible_password is the password for the credential. 

### Ansible 'hosts' File
See [hosts](hosts) file for more information.

Running multiple playbooks on a single playbook gives advantages when you have multiple playbooks to run. The case study includes a master playbook to run all playbook at the yaml folder. The command to execute the playbook is: 
```
$ ansible-playbook playbook.yaml -bK
```

The Case Study includes the following playbooks:
-	acl_config.yaml
-	ansible_test.yaml
-	backup_running_configs.yaml
-	get_ipadd.yaml
-	get_iproute.yaml
-	ospf_config.yaml

### Google Drive Link: https://drive.google.com/drive/folders/1XBc289y3kqMZIKYxBmMIj48j9XH7_WHS?usp=sharing
### Video Simulation: https://drive.google.com/file/d/1H87uaYmgNnBLVT9bNKAKO0kSb3sT4EhM/view?usp=sharing
