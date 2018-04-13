### Install Vagrant using KVM on RHEL/CentOS 64-bit

Tested on CentOS 7.3 1610-01. Vagrantfile *not* tested with KVM.

```shell
# Generate SSH key to use when accessing machines
ssh-keygen -t rsa -b 4096 -N "" -C "root@example.com" -f ~/.ssh/rhce # empty password

# Make loading SSH key to ssh agent automatic
eval $(ssh-agent); echo $'eval $(ssh-agent)' >> ~/.bash_profile
ssh-add ~/.ssh/rhce; echo $'ssh-add ~/.ssh/rhce' >> ~/.bash_profile

# Get latest vagrant version
# which of the following 3 is easiest to maintain and has most chance to fail gracefully when content or url change?
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -nr '/.*href="\/vagrant\/([^/]*).*/{s//\1/p;q}' ` # from top of page
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | awk 'match($0, /href="\/vagrant\/([^/]*)/, a) {print a[1]; exit}'` # pick top version listed on page
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | awk 'match($0, /href="\/vagrant\/([^/]*)/, a)  {if (RSTART)  { ++i; v[i]=a[1]}} END {n = asort (v); print v[n]}'`
# Install packages
sudo yum -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm git qemu libvirt libvirt-devel ruby-devel gcc qemu-kvm

# Install vagrant libvirt plugin
vagrant plugin install vagrant-libvirt ; echo $'vagrant plugin install vagrant-libvirt'>> ~/.bash_profile
```
