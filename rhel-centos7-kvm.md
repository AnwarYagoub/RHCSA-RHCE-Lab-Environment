### Install Vagrant using KVM on RHEL/CentOS 64-bit


```shell
# Generate SSH key to use when accessing machines
ssh-keygen -t rsa -b 4096 -N "" -C "root@example.com" -f ~/.ssh/rhce # empty password

# Make loading SSH key to ssh agent automatic
eval $(ssh-agent); echo $'eval $(ssh-agent)' >> ~/.bash_profile
ssh-add ~/.ssh/rhce; echo $'ssh-add ~/.ssh/rhce' >> ~/.bash_profile

# Get latest vagrant version
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -n 's/.*href="\([^"]*\)".*/\1/p' | sort -r | head -1 | sed 's/[\/|vagrant]//g'`

# Install packages
yum -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm git qemu libvirt libvirt-devel ruby-devel gcc qemu-kvm

# Install vagrant libvirt plugin
vagrant plugin install vagrant-libvirt ; echo $'vagrant plugin install vagrant-libvirt'>> ~/.bash_profile

# Download (clone) lab environment from GitHub
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd RHCSA-RHCE-Lab-Environment/
```

If RHEL/CentOS runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
