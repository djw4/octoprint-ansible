# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.vm.network "forwarded_port", guest: 80, host: 5080
  config.vm.synced_folder "ansible/", "/etc/ansible"
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y -q
    sudo apt-get install -y -q python3-pip python3-dev python3-setuptools python3-venv git libyaml-dev
    python3 -m pip install --quiet --upgrade ansible
  SHELL
  
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "/etc/ansible/install_octoprint.yaml"
  end
end
