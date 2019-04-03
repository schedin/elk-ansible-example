# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/centos7"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 4096
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  
  # ELK server.
  config.vm.define "logs" do |logs|
    logs.vm.hostname = "logs"
    logs.vm.network :private_network, ip: "192.168.9.90"

    logs.vm.provision :ansible do |ansible|
      ansible.playbook = "elk_playbook.yml"
      ansible.become = true
    end
  end
  
end
