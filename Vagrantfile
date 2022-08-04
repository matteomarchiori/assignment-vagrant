# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.box_check_update = true
  
    config.vm.provider "virtualbox" do |virtualbox|
      virtualbox.name = "battleship"
      virtualbox.gui = false
      virtualbox.memory = "1024" # MB
    end
  
    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.network "forwarded_port", guest: 1234, host: 1234
    config.vm.network "forwarded_port", guest: 1235, host: 1235
    config.vm.network "private_network", ip: "192.168.56.2"
    #config.vm.synced_folder "./data", "/host_data"
  
    #config.vm.provision "shell", inline: <<-SHELL
    #  apt update
    #  apt install -y nginx
    #SHELL

    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provision.yml"
      ansible.verbose = "v"
      ansible.extra_vars = {
        "ansible_ssh_user": "vagrant",
        "ansible_ssh_private_key_file": ".vagrant/machines/default/virtualbox/private_key",
        "ansible_become": true,
        "ansible_become_user": "root",
        "ansible_python_interpreter": "/usr/bin/python3"
      }
    end
  end