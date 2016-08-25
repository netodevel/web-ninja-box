# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.define 'webninja' do |machine|
      machine.vm.box = "ubuntu/trusty64"
      machine.vm.hostname = 'webninjabox'
      machine.vm.network "private_network", ip: "10.0.10.50"
      machine.vm.network "forwarded_port", guest: 3000, host: 3000

#      config.vm.synced_folder "../vagrant", "/home/devel"
     
      machine.vm.provision "ansible" do |ansible|
          ansible.playbook = "provisioning/playbook.yml"
          ansible.limit = 'all'
          ansible.verbose = "vvv"
          ansible.sudo = "true"
      end

      machine.vm.provider "virtualbox" do |v|

        # Use VBoxManage to customize the VM. For example to change memory:
        v.customize ["modifyvm", :id, "--memory", "1024"]
        v.customize ["modifyvm", :id, "--cpuexecutioncap", "95"]
      end
    end

end