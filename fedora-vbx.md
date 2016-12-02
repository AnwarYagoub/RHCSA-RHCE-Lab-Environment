### Install Vagrant using VirtualBox on Fedora 24

Tested for Fedora 24

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

# Get vagrant version
export virtualbox_version=`dnf -y search VirtualBox | grep "VirtualBox-" | sed 's/ : Oracle VM VirtualBox//' | sed 's/.x86_64//' | tail -1`

# Install packages
sudo dnf -y install git gcc make kernel-devel $virtualbox_version

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
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -n 's/.*href="\([^"]*\)".*/\1/p' | sort -r | head -1 | sed 's/[\/|vagrant]//g'`

# Install vagrant
sudo dnf -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm

# Check vagrant version
vagrant --version

# Download (clone) lab environment from GitHub
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd ~/RHCSA-RHCE-Lab-Environment
```

If Fedora runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
