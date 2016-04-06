# -*- mode: ruby -*-
# vi: set ft=ruby :

mem_master = 1024
mem_slaves = 1024

Vagrant.configure(2) do |config|
  
  config.vm.define "master1" do |v|
    v.vm.network :private_network, :ip => "10.0.0.10"
    v.vm.provider :virtualbox do |vbox|
      vbox.memory = mem_master
    end
    v.vm.provider :libvirt do |libvirt|
      libvirt.memory = mem_master
      libvirt.cpus   = 2
      libvirt.driver = "kvm"
      libvirt.nested = true
    end
    v.vm.box = "centos/7"
  end

  config.vm.define "slave1" do |v|
    v.vm.network :private_network, :ip => "10.0.0.20"
    v.vm.provider :virtualbox do |vbox|
      vbox.memory = mem_slaves
    end 
    v.vm.provider :libvirt do |libvirt|
      libvirt.memory = mem_slaves
      libvirt.cpus   = 2
      libvirt.driver = "kvm"
      libvirt.nested = true
    end
    v.vm.box = "centos/7"
	end
  config.vm.define "slave2" do |v|
    v.vm.network :private_network, :ip => "10.0.0.30"
    v.vm.provider :virtualbox do |vbox|
      vbox.memory = mem_slaves
    end 
    v.vm.provider :libvirt do |libvirt|
      libvirt.memory = mem_slaves
      libvirt.cpus   = 2
      libvirt.driver = "kvm"
      libvirt.nested = true
    end
    v.vm.box = "centos/7"
	end 
  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
			ansible.groups = {
				"slaves" => [ "slave1", "slave2" ],
				"master" => [ "master1" ]
			}
      ansible.raw_arguments  = [
        "--forks=500"
      ]
  end 
end
