# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
 
  config.vm.synced_folder "ansible", "/vagrant/ansible"
  
  config.vm.define "ose-infra" do |d|
    d.vm.box = "rhel72-server-base.box"
    d.vm.hostname = "ose-infra.example.com"
    d.vm.network "private_network", ip: "10.100.192.201"
    d.vm.provider "virtualbox" do |v|
      v.memory = 2048
    end
    config.vm.provider :virtualbox do |vb|
      vb.gui = true
    end
  end

  (1..1).each do |i|
    config.vm.define "ose-node-#{i}" do |d|
      d.vm.box = "rhel72-server-base.box"
      d.vm.hostname = "ose-node-#{i}.example.com"
      d.vm.network "private_network", ip: "10.100.192.20#{i+1}"
      d.vm.provider "virtualbox" do |v|
        v.memory = 2048
      end
    end
  end

  config.vm.define "ose-master" do |d|
      d.vm.box = "rhel72-server-base.box"
      d.vm.hostname = "ose-master.example.com"
      d.vm.network "private_network", ip: "10.100.192.200"
      d.vm.provider "virtualbox" do |v|
        v.memory = 4096
      end
      d.vm.provision :shell, path: "bootstrap_ansible.sh"
      config.vm.provider "virtualbox" do |v| 
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
      end
      config.vm.provider :virtualbox do |vb|
      vb.gui = true
    end
  end

  config.vm.define "ose-master" do |d|
      d.vm.provision :shell, path: "launch_ansible.sh"
  end


end
