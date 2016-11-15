### Install Vagrant using VirtualBox on Fedora 24

Tested for Fedora 24

Run the following commands on fresh installed Fedora first:
```shell
sudo dnf -y update          # upgrade to the latest kernel etc.
sudo dnf -y install vim
sudo reboot
```

Have you run `dnf update` lately, then start here:
```shell
ssh-keygen -t rsa -b 4096 -N "" -C "root@example.com" -f ~/.ssh/rhce # empty password
eval $(ssh-agent); echo $'eval $(ssh-agent)' >> ~/.bash_profile
ssh-add ~/.ssh/rhce; echo $'ssh-add ~/.ssh/rhce' >> ~/.bash_profile
sudo wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -O /etc/yum.repos.d/virtualbox.repo
sudo dnf clean dbcache
sudo dnf -y repolist        # Import the GPG keys
export virtualbox_version=`dnf -y search VirtualBox | grep "VirtualBox-" | sed 's/ : Oracle VM VirtualBox//' | sed 's/.x86_64//' | tail -1`
sudo dnf -y install git gcc make kernel-devel $virtualbox_version
sudo /sbin/vboxconfig       # load the vboxdrv kernel module, will fail without dnf update
systemctl status vboxdrv    # active?
VBoxManage --version        # should return no errors
sudo reboot
```

```shell
export vagrant_version=`wget --quiet -O - https://releases.hashicorp.com/vagrant/ | sed -n 's/.*href="\([^"]*\)".*/\1/p' | sort -r | head -1 | sed 's/[\/|vagrant]//g'`
sudo dnf -y install https://releases.hashicorp.com/vagrant/"$vagrant_version"/vagrant_"$vagrant_version"_x86_64.rpm
vagrant --version
cd ~
git clone https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment.git
cd ~/RHCSA-RHCE-Lab-Environment
```

If Fedora runs without GUI, then execute these 2 commands:
```shell
sed -i 's/gui\: true/gui\: false/g' provisioning/RHCSA_RHCE_LAB/defaults/main.yml   # no need for gui on commandline
sed -i 's/vb.gui = true/vb.gui = false/g' Vagrantfile # without GUI vagrant will error with 'vb.gui = true'
```
