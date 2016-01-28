# -*- mode: ruby -*-
# vi: set ft=ruby :

num_master = 3;

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "opscode-centos-7.1"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-7.1_chef-provisionerless.box"
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end
  
  (0..(num_master - 1)).each do |i|
    config.vm.define "master-#{i}" do |m|
        m.vm.hostname = "master-#{i}"
        m.vm.network "private_network", ip: "10.100.199.20#{i}"
    end
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "ansible/inventory/vagrant"
    ansible.playbook = "ansible/playbook.yml"
    ansible.verbose = "vvvv"
  end

end