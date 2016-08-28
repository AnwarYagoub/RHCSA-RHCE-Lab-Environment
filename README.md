# Red Hat RHCSA-RHCE 7 Cert Guide (Lab Environment)

## About
This project offers environment for all the labs in **Red Hat RHCSA/RHCE 7 Cert Guide: Red Hat Enterprise Linux 7** book written  by Sander Van Vugt.

## What is included?
- server1: CentOS box (Server With GUI).
- server2: same as Server1
- cache-server: Debian box used for package caching.
- FreeIPA: CentOS box with FreeIPA configured.

## IP addresses
| Server | IP address |
|---|---|
|cache-server|192.168.122.100 |
|server1|192.168.122.210|
|server2|192.168.122.220|
|FreeIPA|192.168.122.200|

## install dependencies:
- Virtualbox.
- Vagrant.
- Ansible.
<br>
### 1. Install [Virtualbox](https://www.virtualbox.org) :

**1.1 Install virtualbox on Ubuntu:**

```shell
$ wget -q -O - http://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc | sudo apt-key add -

$ sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian `lsb_release -sc` non-free contrib" > /etc/apt/sources.list.d/virtualbox.org.list' 

$ sudo apt-get update
	
$ sudo apt-get install dkms 

$ sudo apt-get install virtualbox-5.1
```
**1.2 Install virtualbox on Oracle Linux/RHEL/CentOS:**
```shell
$ wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | rpm --import -

$ sudo wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo

$ sudo yum install VirtualBox-5.1
```

**1.3 Install virtualbox on Fedora:**
```shell
$ wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | rpm --import -

$ sudo wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo

$ sudo yum install VirtualBox-5.1
```
<br>
### 2. Install [Vagrant](https://www.vagrantup.com/) :

**2.1 Install vagrant on Debian-based Linux Ubuntu/Mint (64-bit):**
```shell
$ wget https://releases.hashicorp.com/vagrant/1.8.5/vagrant_1.8.5_x86_64.deb

$ sudo dpkg -i vagrant_1.8.5_x86_64.deb
```

**2.2 Install vagrant on Debian-based distributions Ubuntu/Mint (32-bit):**
```shell
$ wget https://releases.hashicorp.com/vagrant/1.8.5/vagrant_1.8.5_i686.deb

$ sudo dpkg -i vagrant_1.8.5_i686.deb
```

**2.3 Install vagrant on RedHat-based distributions (64-bit):**
```shell
$ wget https://releases.hashicorp.com/vagrant/1.8.5/vagrant_1.8.5_x86_64.rpm

$ sudo rpm -ivh vagrant_1.8.5_x86_64.rpm
```

**2.4 Install vagrant on RedHat-based distributions (32-bit):**
```shell
$ wget https://releases.hashicorp.com/vagrant/1.8.5/vagrant_1.8.5_i686.rpm

$ sudo rpm -ivh vagrant_1.8.5_i686.rpm
```
<br>
### 3. Install [Ansible](https://www.ansible.com/) :
**3.1 Install ansible on Debian-based distributions (Ubuntu/Mint):**
```shell
$ sudo apt-get install gcc libssl-dev python-dev python-setuptools

$ sudo easy_install pip

$ sudo pip install ansible netaddr
```

**3.2 Install ansible on RedHat-based distributions:**
```shell
$ sudo yum install gcc openssl-devel python-devel python-setuptools

$ sudo easy_install pip

$ sudo pip install ansible netaddr
```
<br>
## How to use?
- Navigate to project path where Vagranfile exists.
- Run vagrant up command to initiate the environment:
```shell
$ vagrant up
```
