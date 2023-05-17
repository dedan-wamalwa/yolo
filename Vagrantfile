# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.ssh.insert_key = false
  config.vm.provision "ansible" do |ansible|
  ansible.playbook = "playbook.yml"
  end
end
