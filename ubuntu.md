### Ubuntu 16.04
Instructions for installing VirtualBox & Vagrant on Ubuntu 16.04

```shell
sudo apt update
sudo apt -y --force-yes upgrade
sudo reboot
```

```shell
ssh-keygen -t rsa -b 4096 -N "" -C "root@example.com" -f ~/.ssh/rhce # empty password
eval $(ssh-agent); echo $'eval $(ssh-agent)' >> ~/.profile
ssh-add ~/.ssh/rhce; echo $'ssh-add ~/.ssh/rhce' >> ~/.profile
wget -q -O - http://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian `lsb_release -sc` non-free contrib" > /etc/apt/sources.list.d/virtualbox.org.list'
# TODO remove linestarve.com and use alternative method to get latest version of vagrant
sudo bash -c 'echo deb http://vagrant-deb.linestarve.com/ any main > /etc/apt/sources.list.d/wolfgang42-vagrant.list'
sudo apt-key adv --keyserver pgp.mit.edu --recv-key AD319E0F7CFFA38B4D9F6E55CE3F3DE92099F7A4
sudo apt update
# TODO remove virtualbox version-number and automatically install latest version; dkms needed when upgrading kernel
sudo apt -y --force-yes install virtualbox-5.1 git vagrant # virtualbox-ext-pack dkms
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd ~/RHCSA-RHCE-Lab-Environment
```

If ubuntu runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
