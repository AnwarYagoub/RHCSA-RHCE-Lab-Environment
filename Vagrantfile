# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # if vagrant-vbguest is installed stop auto updating virtualbox guest add-on update
  if defined? VagrantVbguest
    config.vbguest.auto_update = false
  end

  # Set language locale environment variables
  ENV['LC_ALL']="en_US.UTF-8"
  ENV['LANG']="en_US.UTF-8"

  # configure cache-server machine
  config.vm.define "cache-server" do |node|
    node.vm.box = "debian/jessie64"
    node.vm.hostname = "cache-server.example.com"
    node.vm.network "private_network", ip: "192.168.4.100"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.name = "cache-server"
    end
    node.vm.provision :ansible_local do |ansible|
      ansible.install_mode = "pip"
      ansible.version = "latest"
      ansible.playbook = "provisioning/cache-server.yml"
    end
  end

  # configure labipa machine
  config.vm.define "labipa" do |node|
    # machine basic settings
    node.vm.box = "centos/7"
    node.vm.hostname = "labipa.example.com"
    node.vm.network "private_network", ip: "192.168.4.200", auto_config: false
    # provider specific settings
    node.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = "2048"
      vb.name = "labipa"
    end
    # provision machine using ansible
    node.vm.provision :ansible_local do |ansible|
      ansible.install_mode = "pip"
      ansible.version = "latest"
      ansible.host_vars = { "labipa" => { "private_ipv4_address" => "192.168.4.200" , "private_ipv6_address" => "fd00::200" }}
      ansible.playbook = "provisioning/labipa.yml"
    end
  end

  # configure two machines server1 & server2
  (1..2).each do |i|
    config.vm.define "server#{i}" do |node|

      # machine basic settings
      node.vm.box = "centos/7"
      # node.vm.box_version = "1509.01"
      node.vm.hostname = "server#{i}.example.com"
      # yes this is a bug in Vagrant: we need to provide the ip-address even if auto_config doesn't use it
      node.vm.network "private_network", ip: "192.168.4.2#{i}0", auto_config: false
      # provider specific settings
      node.vm.provider "virtualbox" do |vb|
        vb.gui = true
        vb.memory = "1024"
        # Get disk path
        vb.name = "server#{i}"
        line = `VBoxManage list systemproperties | grep "Default machine folder"`
        vb_machine_folder = line.split(':')[1].strip()
        disk_name = "disk2.vdi"
        second_disk = File.join(vb_machine_folder, vb.name, disk_name)
        # Add another Hard Disk which is 1 GB in size
        unless File.exist?(second_disk)
          vb.customize ['createhd', '--filename', second_disk, '--variant', 'Fixed', '--size', 1 * 1024]
          vb.customize ["storagectl", :id, "--name", "SATA Controller", "--add", "sata"]
        end
        # attach the new Hard Disk
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', second_disk]
      end

      # provision machine using ansible
      node.vm.provision :ansible_local do |ansible|
        ansible.install_mode = "pip"
        ansible.version = "latest"
        ansible.host_vars = { "server#{i}" => { "private_ipv4_address" => "192.168.4.2#{i}0" , "private_ipv6_address" => "fd00::2#{i}0" } }
        ansible.playbook = "provisioning/servers.yml"
      end

    end
  end

end
