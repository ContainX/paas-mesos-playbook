# -*- mode: ruby -*-
# vi: set ft=ruby :

# Debian - oar-team/debian8
# Ubuntu - ubuntu/trusty64, ubuntu/vivid64
# CentOS - centos/7

vm_box = "ubuntu/trusty64"

Vagrant.configure("2") do |config|
  # config.vm.provider "virtualbox" do |v|
  #   v.memory = 4096
  #   v.cpus = 1
  # end

  config.ssh.insert_key = false

  config.vm.define 'master' do |c|
    c.vm.network "private_network", ip: "10.142.142.10"
    c.vm.box = vm_box
    c.vm.hostname = "master"
    c.vm.provider "virtualbox" do |v|
      v.memory = 1048
      v.cpus = 1
    end
  end

 # config.vm.define 'master2' do |c|
 #    c.vm.network "private_network", ip: "10.142.142.11"
 #    c.vm.box = vm_box
 #    c.vm.hostname = "master2"
 #    c.vm.provider "virtualbox" do |v|
 #      v.memory = 1048
 #      v.cpus = 1
 #    end
 #  end

  ## Update to the count defined in the 'vagrant' file for slaves
  num_slaves = 2

  (1..num_slaves).each do |num|
    config.vm.define "slave#{num}" do |c|
      c.vm.network "private_network", ip: "10.142.142.2#{num}"
      c.vm.box = vm_box
      c.vm.hostname = "slave#{num}"

      c.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
      end

      if num == num_slaves
        c.vm.provision "ansible" do |ansible|
          ansible.verbose = "vv"
          ansible.playbook = "site.yml"
          ansible.inventory_path = "./vagrant"
          ansible.limit = 'all'
          ansible.host_key_checking = false
          ansible.extra_vars = {
            docker_install_recommended_package: false
          }
        end
      end
    end
  end
end
