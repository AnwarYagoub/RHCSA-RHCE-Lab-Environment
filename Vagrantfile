# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # configure two machines server1 & server2
  (1..2).each do |i|
    config.vm.define "server#{i}" do |node|
      node.vm.box = "centos/7"
      node.vm.hostname = "server#{i}"
      node.vm.network "private_network", ip: "192.168.4.1#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
      end
    end
  end

  config.vm.define "FreeIPA" do |node|
    node.vm.box = "centos/7"
    node.vm.hostname = "freeipa"
    node.vm.network "private_network", ip: "192.168.4.13"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.gui = true
    end
  end

  config.vm.define "cache-server" do |node|
    node.vm.box = "ubuntu/trusty64"
    node.vm.hostname = "cache-server"
    node.vm.network "private_network", ip: "192.168.4.10"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = "256"
    end
    node.vm.provision "shell",
      inline: "sudo apt-get update && apt-get upgrade -y && apt-get install -y apt-cacher-ng"
  end

end
