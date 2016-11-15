### RHEL/CentOS 64-bit
```shell
sudo wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo
sudo yum clean dbcache; yum -y repolist    # Import the GPG keys
sudo yum -y install epel-release           # should be 7.8
export virtualbox_version=`yum -y search VirtualBox | grep "VirtualBox-" | sed 's/ : Oracle VM VirtualBox//' | sed 's/.x86_64//' | tail -1`
sudo yum -y install git gcc make kernel-devel $virtualbox_version
sudo /sbin/vboxconfig                      # load the vboxdrv kernel module
systemctl status vboxdrv              # enabled?
VBoxManage --version                  # should return no errors
sudo reboot
```

```shell
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -n 's/.*href="\([^"]*\)".*/\1/p' | sort -r | head -1 | sed 's/[\/|vagrant]//g'`
yum -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm
vagrant --version
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd ~/RHCSA-RHCE-Lab-Environment
```

If RHEL/CentOS runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
