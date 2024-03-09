# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  (1..2).each do |i|
    config.vm.define "node-#{i}" do |node|
      #if you not want to run in /mnt/c use this config
      node.vm.synced_folder '.', '/vagrant', disabled: true

      node.vm.box = "ubuntu/focal64"
      node.vm.hostname = "node-#{i}"
      node.vm.network "private_network", ip: "192.168.56.#{i+10}"
      node.vm.provision "shell", inline: "sudo apt update"
      if Vagrant.has_plugin?("vagrant-vbguest")
        node.vbguest.auto_update = false
      end       
      node.vm.provider "virtualbox" do |v|
        v.check_guest_additions = false
        v.memory = 2048
        v.cpus = 2
        #to avoid error during start vm
        v.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
      end
    end
  end
end
