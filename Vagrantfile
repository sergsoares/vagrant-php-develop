# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  config.vm.synced_folder "projects/", "/projects"
  config.vm.synced_folder "containers", "/containers"

  config.vm.network "forwarded_port", host: 8080 ,guest: 8080
  config.vm.network "forwarded_port", host: 3306, guest: 3306 
  config.vm.network "forwarded_port", host: 6379 ,guest: 6379 
  config.vm.network "forwarded_port", host: 27017 ,guest: 27017 
  config.vm.network "forwarded_port", host: 27017 ,guest: 27017 
  config.vm.network "forwarded_port", host: 9200 ,guest: 9200 

  config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
  end

   config.vm.provision "shell", inline: <<-SHELL
     curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
     sudo usermod -aG docker vagrant
     sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
   SHELL

   config.vm.provision "shell", run: "always", inline: <<-SHELL
     docker-compose -f /vagrant/docker-compose.yml up
   SHELL
end
