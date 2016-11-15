### Ubuntu 16.04
Instructions for installing VirtualBox & Vagrant on Ubuntu 16.04

TODO: test this procedure
```shell
# TODO create ~/.ssh/rhce and ssh-add
wget -q -O - http://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian `lsb_release -sc` non-free contrib" > /etc/apt/sources.list.d/virtualbox.org.list'
sudo apt-get update
sudo apt-get install dkms
sudo apt-get install virtualbox-5.1
sudo apt-get git
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd ~/RHCSA-RHCE-Lab-Environment
```

If ubuntu runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
