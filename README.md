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

## How to use?
- Install [Virtualbox](https://www.virtualbox.org) & [Vagrant](https://www.vagrantup.com/) in your machine.

- Navigate to project path where Vagranfile exists.

- Run vagrant up command to initiate the environment:
```shell
$ vagrant up
```
