# -*- mode: ruby -*-
# vi: set ft=ruby :

# Overwrite host locale in vagrant ssh session
# ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  # config.vm.box_check_update = false
  config.vm.hostname = "VPS"
  # config.vm.network "private_network", ip: "192.168.99.100"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.synced_folder "www/", "/var/www", create: true, owner: "www-data", group: "www-data", mount_options: ["dmode=755,fmode=644"]
  config.ssh.username = "vagrant"
  config.ssh.private_key_path=["~/.vagrant.d/insecure_private_key"]
  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "4096"
    vb.cpus   = "2"
    vb.name   = "VPS"
  end
  config.vm.provision :file do |file|
    file.source = "./Scripts/ServerBuilding"
    file.destination = "~/.local/bin/ServerBuilding"
  end
  config.vm.provision :shell, name: "Executable file", inline: <<-SHELL
    source /home/vagrant/.profile
    chmod +x /home/vagrant/.local/bin/ServerBuilding
  SHELL
end
