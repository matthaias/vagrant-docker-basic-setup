# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure(2) do |config|
  
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get autoremove -y
    wget -qO- https://get.docker.com/ | sh
    sudo usermod -aG docker vagrant
    curl -L https://github.com/docker/compose/releases/download/1.3.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
  SHELL
   
  config.vm.define "lb" do |lb|
    lb.vm.box = "ubuntu/trusty64"
    lb.vm.network "private_network", ip: "192.168.50.101"
    lb.vm.provision "shell", inline: "sudo docker pull nginx:latest"
    lb.vm.provision "shell", inline: "cd /vagrant/nginx && docker-compose up -d"
  end

  config.vm.define "engine1" do |engine1|
    engine1.vm.box = "ubuntu/trusty64"
    engine1.vm.network "private_network", ip: "192.168.50.102"
    engine1.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
    engine1.vm.provision "shell", inline: "sudo docker pull iojs:latest"
    engine1.vm.provision "shell", inline: "sudo docker pull mongo:latest"
    engine1.vm.provision "shell", inline: "sudo docker pull redis:latest"
  end
  
  config.vm.define "engine2" do |engine2|
    engine2.vm.box = "ubuntu/trusty64"
    engine2.vm.network "private_network", ip: "192.168.50.103"
    engine2.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
    engine2.vm.provision "shell", inline: "sudo docker pull iojs:latest"
    engine2.vm.provision "shell", inline: "sudo docker pull mongo:latest"
    engine2.vm.provision "shell", inline: "sudo docker pull redis:latest"
  end
  
end