### Instructions for installing VirtualBox & Vagrant on Ubuntu

Tested on Ubuntu 16.04

```shell
# Update packages list
sudo apt update

# Upgrade Ubuntu & cleanup
sudo apt -y upgrade; sudo apt -y autoremove

# Reboot machine
sudo reboot
```

```shell
# Generate SSH key to use when accessing machines
ssh-keygen -t rsa -b 4096 -N "" -C "root@example.com" -f ~/.ssh/rhce # empty password

# Make loading SSH key to ssh agent automatic
eval $(ssh-agent); echo $'eval $(ssh-agent)' >> ~/.profile
ssh-add ~/.ssh/rhce; echo $'ssh-add ~/.ssh/rhce' >> ~/.profile

# Add Virtualbox GPG Key & repository
wget -q -O - http://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian `lsb_release -sc` non-free contrib" > /etc/apt/sources.list.d/virtualbox.org.list'
export ubuntu_codename=`lsb_release -sc`
# which of the following 2 is easiest to maintain, has most chance to fail gracefully when yum implementation changes or Vbox gets new numbering scheme  
export virtualbox_version=`wget --quiet -O - http://download.virtualbox.org/virtualbox/debian/dists/$ubuntu_codename/contrib/binary-amd64/Packages | awk 'match($0, /(virtualbox-[0-9]\.[0-9])/, a) {b=a[1]} END {print b}'` # depends on sorting in Packages file
export virtualbox_version=`wget --quiet -O - http://download.virtualbox.org/virtualbox/debian/dists/$ubuntu_codename/contrib/binary-amd64/Packages | awk 'match($0, /(virtualbox-[0-9]\.[0-9])/, a)  {if (RSTART)  { ++i; v[i]=a[1]}} END {n = asort (v); print v[n]}'`

# Get latest vagrant version
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -nr '/.*href="\/vagrant\/([^/]*).*/{s//\1/p;q}' ` # from top of page
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | awk 'match($0, /href="\/vagrant\/([^/]*)/, a)  {if (RSTART)  { ++i; v[i]=a[1]}} END {n = asort (v); print v[n]}'`
wget https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.deb -O vagrant_"$vagrant_version"_x86_64.deb

# Update packages list
sudo apt update

# Install packages
sudo apt -y install $virtualbox_version git ./vagrant_"$vagrant_version"_x86_64.deb; rm ./vagrant_"$vagrant_version"_x86_64.deb
```
