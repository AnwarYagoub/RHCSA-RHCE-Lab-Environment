# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # configure two machines server1 & server2
  (1..2).each do |i|
    config.vm.define "server#{i}" do |node|

      # machine basic settings
      node.vm.box = "centos/7"
      node.vm.hostname = "server#{i}"
      node.vm.network "private_network", ip: "192.168.122.1#{i}"

      # provider specific settings
      node.vm.provider "virtualbox" do |vb|
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
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/servers.yml"
      end

    end
  end

  config.vm.define "FreeIPA" do |node|
    # machine basic settings
    node.vm.box = "centos/7"
    node.vm.hostname = "freeipa"
    node.vm.network "private_network", ip: "192.168.122.200"
    # provider specific settings
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.name = "FreeIPA"
      vb.gui = true
    end
    # provision machine using ansible
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/freeipa.yml"
    end
  end

  config.vm.define "cache-server" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.hostname = "cache-server"
    node.vm.network "private_network", ip: "192.168.122.100"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.name = "cache-server"
    end
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/cache-server.yml"
    end
  end

end
