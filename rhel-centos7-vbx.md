### RHEL/CentOS 64-bit
```shell
# Download VirtualBox repository
sudo wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo

# Clean repository cache & import GPG Key
sudo yum clean dbcache; sudo yum -y repolist    # Import the GPG keys

# Ensure latest version of Extra Packages for Enterprise Linux is installed
sudo yum -y install epel-release           # should be 7.8

# Get vagrant version
export virtualbox_version=`yum -y search VirtualBox | grep "VirtualBox-" | sed 's/ : Oracle VM VirtualBox//' | sed 's/.x86_64//' | tail -1`

# Install packages
sudo yum -y install git gcc make kernel-devel $virtualbox_version

# Install VirtualBox kernel modules
sudo /sbin/vboxconfig                      # load the vboxdrv kernel module

# Check if vboxdrv service is started without errors
systemctl status vboxdrv              # enabled?

# Check VirtualBox version
VBoxManage --version                  # should return no errors

# Restart machine
sudo reboot
```

```shell
# Get latest vagrant version
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -nr 's/.*href="\/vagrant\/([^/]*).*/\1/p' |  head -1 `

# Install vagrant
sudo yum -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm

# Check vagrant version
vagrant --version

# Download (clone) lab environment from GitHub
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd ~/RHCSA-RHCE-Lab-Environment
```

If RHEL/CentOS runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
