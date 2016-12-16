
Tested on Windows 8.1 & Windows 10

# Prerequisites:
1. [VirtualBox][virtualBox] Visualization Software.
2. [Vagrant][vagrant] Software for building and maintaining portable virtual development environments.
3. Optional [PuTTY][PuTTY] SSH client since Windows does't natively have one.


There are two Installation methods available for MS.Windows:

- [Regular "Download and Install".](#regular-download-and-install)
- [Using a package manager for Windows like Chocolatey.](#windows-package-manager)


## Regular "download and install":
This method is well-known to Windows users, all you need to do is download
[VirtualBox][virtualBox-download], [Vagrant][vagrant-download] and optionally
[PuTTY][PuTTY-download].

Next, Install in the same **order**, VirtualBox then Vagrant.
***Note1: You need to have Visualization/Hyper-V Supported and Enabled***


***Note2: In Case you need to update both Vagrant and VirtualBox You need
to _REMOVE_ both then re-installing them in same order above to prevent
errors and failures my occur during update***


## Windows Package Manager:
This method may be new to some Windows users but its much more easier to install
and maintain since it blows away the D&I old method and make ease updating
packages for Windows. One good Windows package manager is [Chocolaty][Chocolaty].

You can find installation Guide in [Chocolaty official website][Chocolaty-install].
After Installing Chocolaty Install VirtualBox, Vagrant and optionally PuTTY
using the following commands with __administrator Privileges__:

```powershell
choco install virtualbox

choco install vagrant

choco install putty
```


[virtualBox]: https://www.virtualbox.org/
[virtualBox-download]: https://www.virtualbox.org/wiki/Downloads
[vagrant]: https://www.vagrantup.com/
[vagrant-download]: https://www.vagrantup.com/downloads.html
[PuTTY]: http://www.chiark.greenend.org.uk/~sgtatham/putty/
[PuTTY-download]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[Chocolaty]: http://chocolatey.org/
[Chocolaty-install]: https://chocolatey.org/install