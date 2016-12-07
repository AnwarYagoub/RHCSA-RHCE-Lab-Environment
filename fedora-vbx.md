### Install Vagrant using VirtualBox on Fedora 25

Tested for Fedora 25

Run the following commands on fresh installed Fedora first:
```shell
# Upgrade fedora
sudo dnf -y update          # upgrade to the latest kernel etc.

# Install vim editor
sudo dnf -y install vim

# Reboot machine
sudo reboot
```

Have you run `dnf update` lately, then start here:
```shell
# Generate SSH key to use when accessing machines
ssh-keygen -t rsa -b 4096 -N "" -C "root@example.com" -f ~/.ssh/rhce # empty password

# Make loading SSH key to ssh agent automatic
eval $(ssh-agent); echo $'eval $(ssh-agent)' >> ~/.bash_profile
ssh-add ~/.ssh/rhce; echo $'ssh-add ~/.ssh/rhce' >> ~/.bash_profile

# Download VritualBox repository
sudo wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo

# Clean repository cache & import GPG Key
sudo dnf clean dbcache
sudo dnf -y repolist        # Import the GPG keys

# Install lastest virtualbox; will error when multiple versions of virtualbox are offered.
sudo dnf -y install git gcc make kernel-devel VirtualBox*

# Install VirtualBox kernel modules
sudo /sbin/vboxconfig       # load the vboxdrv kernel module, will fail without dnf update

# Check if vboxdrv service is started without errors
systemctl status vboxdrv    # active?

# Check VirtualBox version
VBoxManage --version        # should return no errors

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
sudo dnf -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm

# Check vagrant version
vagrant --version
```
