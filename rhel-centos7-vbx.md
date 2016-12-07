### Install Vagrant using VirtualBox on RHEL/CentOS 64-bit

Tested on CentOS 7.3 1610-01

```shell
# Download VirtualBox repository
sudo wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo

# Clean repository cache & import GPG Key
sudo yum clean dbcache; sudo yum -y repolist    # Import the GPG keys

# Ensure latest version of Extra Packages for Enterprise Linux is installed
sudo yum -y install epel-release      # should be 7.8

# Get latest VirtualBox version
# which of the following 2 is easiest to maintain, has most chance to fail gracefully when yum implementation changes or Vbox gets new numbering scheme  
export virtualbox_version=`yum -y search VirtualBox | awk 'match($0, /(VirtualBox-[0-9]\.[0-9])/, a) {b=a[1]} END {print b}'`  # depends on yum sorting
export virtualbox_version=`yum -y search VirtualBox | awk 'match($0, /(VirtualBox-[0-9]\.[0-9])/, a)  {if (RSTART)  { ++i; v[i]=a[1]}} END {n = asort (v); print v[n]}'`

# Install packages
sudo yum -y install git gcc make kernel-devel $virtualbox_version

# Install VirtualBox kernel modules
sudo /sbin/vboxconfig                 # load the vboxdrv kernel module

# Check if vboxdrv service is started without errors
systemctl status vboxdrv              # enabled?

# Check VirtualBox version
VBoxManage --version                  # should return no errors

# Restart machine
sudo reboot
```

```shell
# Get latest vagrant version
# which of the following 3 is easiest to maintain and has most chance to fail gracefully when content or url change?
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -nr '/.*href="\/vagrant\/([^/]*).*/{s//\1/p;q}' ` # from top of page
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | awk 'match($0, /href="\/vagrant\/([^/]*)/, a) {print a[1]; exit}'` # pick top version listed on page
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | awk 'match($0, /href="\/vagrant\/([^/]*)/, a)  {if (RSTART)  { ++i; v[i]=a[1]}} END {n = asort (v); print v[n]}'`

# Install vagrant
sudo yum -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm

# Check vagrant version
vagrant --version
```
