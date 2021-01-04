# -*- mode: ruby -*-
# vi: set ft=ruby :

#  https://github.com/rapid7/metasploitable3

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true

  config.vm.define "ub1404" do |pentester|
    pentester.vm.box = "galaxy3/bahryn"
    pentester.vm.box_version = "2021.01.04-0851"
    pentester.vm.hostname = "tattoine"
    pentester.ssh.username = 'vagrant'
    pentester.ssh.password = 'vagrant'

    pentester.vbguest.auto_update = false
    pentester.ssh.insert_key = false
    pentester.ssh.connect_timeout = 20
    pentester.vm.boot_timeout = 120

    pentester.vm.network "private_network", ip: '10.55.56.52',
    	virtualbox__intnet: "metasploitable3",
    	nic_type: "virtio"

    pentester.vm.provider "virtualbox" do |v|
      v.name = "Bahryn (shellshock)"
#      v.memory = 2048

      #v.customize ['modifyvm', :id, '--nic0', 'intnet']
#      v.customize ['modifyvm', :id, '--nictype0', 'virtio']
#      v.customize ['modifyvm', :id, '--nicpromisc0', 'allow-all']


#      v.customize ['modifyvm', :id, '--nictype1', 'virtio']
#      v.customize ['modifyvm', :id, '--nicpromisc1', 'allow-all']
#      v.customize ['modifyvm', :id, '--nictype2', 'virtio']
#      v.customize ['modifyvm', :id, '--nicpromisc2', 'allow-all']
#      v.customize ['modifyvm', :id, '--nictype3', 'virtio']
#      v.customize ['modifyvm', :id, '--nicpromisc3', 'allow-all']
    end
  end

end
