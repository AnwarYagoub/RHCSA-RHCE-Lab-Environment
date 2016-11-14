# Red Hat RHCSA-RHCE 7 Cert Guide (Lab Environment)

## About
This project offers environment for all the labs in **Red Hat RHCSA/RHCE 7 Cert Guide: Red Hat Enterprise Linux 7** book written by Sander van Vugt.

## What is included?
- server1: CentOS box (Server With GUI).
- server2: same as Server1
- cache-server: Debian box used for package caching.
- labipa: CentOS box with FreeIPA configured.

## install dependencies:
- [Virtualbox](https://www.virtualbox.org): cross-platform virtualization application.
- [Vagrant](https://www.vagrantup.com): tool for building complete development environments. With an easy-to-use workflow and focus on automation

Don't worry you don't have to be expert on any of these tools.
### 1. Install virtualbox :

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
### 2. Install vagrant :

**2.1 Install vagrant on Debian-based Linux Ubuntu/Mint (64-bit):**
```shell
$ wget https://releases.hashicorp.com/vagrant/1.8.7/vagrant_1.8.7_x86_64.deb

$ sudo dpkg -i vagrant_1.8.6_i686.deb
```

**2.2 Install vagrant on Debian-based distributions Ubuntu/Mint (32-bit):**
```shell
$ wget https://releases.hashicorp.com/vagrant/1.8.7/vagrant_1.8.7_i686.deb

$ sudo dpkg -i vagrant_1.8.6_i686.deb
```

**2.3 Install vagrant on RedHat-based distributions (64-bit):**
```shell
$ sudo yum -y install https://releases.hashicorp.com/vagrant/1.8.7/vagrant_1.8.7_x86_64.rpm
```

**2.4 Install vagrant on RedHat-based distributions (32-bit):**
```shell
$ sudo yum -y install https://releases.hashicorp.com/vagrant/1.8.7/vagrant_1.8.7_i686.rpm
```

## Get environment
```shell
$ git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git

$ cd RHCSA-RHCE-Lab-Environment
```
## How to start servers?
Navigate to project path where Vagranfile exists.

- start all servers
```shell
$ vagrant up
```
- start a specific server
```shell
$ vagrant up MACHINE_NAME
```
replace **MACHINE_NAME** with any of (server1, server2, cache-server, labipa)
```shell
$ vagrant up server1
```
## How to access servers?
Navigate to project path where Vagranfile exists.

- to get shell access to any of environment servers
```shell
$ vagrant ssh MACHINE_NAME
```
replace **MACHINE_NAME** with any of (server1, server2, cache-server, labipa)
```shell
$ vagrant ssh server1
```
- You can also access servers using ip addresses listed below.
```shell
ssh root@192.168.4.210
```
## How to stop servers?
Navigate to project path where Vagrantfile exists.

- stop all servers
```shell
$ vagrant halt
```
- stop a specific server
```shell
$ vagrant halt MACHINE_NAME
```
replace **MACHINE_NAME** with any of (server1, server2, cache-server, labipa)
```shell
$ vagrant halt server1
```

## IP addresses & credentials
| Server | IP address | username | password | username | password |
|---|---|:---:|:---:|:---:|:---:|
|cache-server|192.168.4.100 |vagrant|vagrant| | |
|server1|192.168.4.210|user|password|root|password|
|server2|192.168.4.220|user|password|root|password|
|labipa|192.168.4.200 |user|password|root|password|
