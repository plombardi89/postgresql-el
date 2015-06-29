# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'

$bootstrap_script=<<SCRIPT
#!/bin/bash -eux
sudo yum -y install epel-release
sudo yum -y update
sudo yum -y install gcc python-devel python-pip
sudo yes | pip install ansible
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'chef/centos-7.0'
  
  config.vm.network :forwarded_port, guest: 5432, host: 5432
  
  config.vm.provision :shell, inline: $bootstrap_script
  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'role.yml'
    ansible.extra_vars = {
      ansible_ssh_user: 'vagrant' 
    }
  end
end