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

Follow the individual instructions for your platform:
- RHEL/Centos 7 with [VirtualBox](rhel-centos7-vbx.md) or [KVM](rhel-centos7-kvm.md)
- [Fedora](fedora-vbx.md)
- macOS TODO
- [Ubuntu](ubuntu.md)
- Windows TODO


## How to start servers?
Navigate to project path where Vagranfile exists.

- setup all servers
```shell
cd ~/RHCSA-RHCE-Lab-Environment
vagrant up                  # create all machines, may take 10-60 minutes
ssh-keygen -R 192.168.4.200; ssh-copy-id root@192.168.4.200
ssh-keygen -R 192.168.4.210; ssh-copy-id root@192.168.4.210
ssh-keygen -R 192.168.4.220; ssh-copy-id root@192.168.4.220
vagrant halt                # shutdown all machines
vagrant status              # all 4 have state poweroff
vagrant snapshot save begin # create a VM snapshot
```

- start all servers
```shell
vagrant snapshot restore begin --no-provision
```

- start a specific server
```shell
vagrant snapshot restore MACHINE_NAME begin --no-provision
```
replace **MACHINE_NAME** with any of (server1, server2, cache-server, labipa)

## How to access servers?
Navigate to project path where Vagrantfile exists.

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
