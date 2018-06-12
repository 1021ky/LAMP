# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box="ubuntu/xenial64"

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://{proxy_ip}:{proxy_port}"
    config.proxy.https    = "http://{proxy_ip}:{proxy_port}"
    config.proxy.no_proxy = "localhost,127.0.0.1"
  end


  # TODO: try nfs sync for windows
  config.vm.define "web1" do |machine|
    machine.vm.provision "shell", inline: <<-SHELL
      apt install -y -qq python
    SHELL

    machine.vm.hostname = "web1"
    machine.vm.synced_folder "./www", "/var/www/html"
    machine.vm.synced_folder "./log", "/vagrant/log", create: true
    
    machine.vm.network :private_network, ip:"192.168.20.10"
    machine.vm.network "forwarded_port", guest: 80, host: 8080
    machine.vm.provider "virtualbox" do |vb|
      vb.memory = "1028"
      vb.cpus=1
    end
  end

  config.vm.define "db1" do |machine|
    machine.vm.provision "shell", inline: <<-SHELL
      apt install -y -qq python
    SHELL

    machine.vm.hostname = "db1"

    machine.vm.network :private_network, ip:"192.168.20.11"
    machine.vm.network "forwarded_port", guest: 3606, host: 3606  
    machine.vm.provider "virtualbox" do |vb|
      vb.memory = "1028"
      vb.cpus=1
    end
  end

  # TODO 完成後 , autostart: falseを入れておく。一度だけ立ててprovisioningすればよいので。
  config.vm.define "controller" do |machine|
    machine.vm.network "private_network", ip: "192.168.20.100"
    machine.vm.synced_folder "./playbook", "/vagrant/playbook",  mount_options: ['dmode=744','fmode=744']
    machine.vm.provision :ansible_local do |ansible|
      ansible.inventory_path = "playbook/inventory/hosts"
      ansible.playbook       = "playbook/playbook.yml"
      ansible.config_file    = "playbook/ansible.cfg"
      ansible.install_mode   = :pip
      ansible.version        = "2.4.0.0" # needs to set install_mode :pip
      ansible.verbose        = true
      ansible.limit          = "all" # or group
    end
  end
end
 