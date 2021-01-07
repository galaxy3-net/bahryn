# -*- mode: ruby -*-
# vi: set ft=ruby :

#  https://github.com/rapid7/metasploitable3



# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true

#  config.trigger.after :up do |trigger|
#    trigger.name = "Complete Setup"
#  	trigger.info = File.read("Description")
#  end

  config.vm.provision "file", source: "playbook.yml", destination: "playbook.yml"
  config.vm.provision "file", source: "../../functions", destination: "functions/bin"
  config.vm.provision "file", source: "hosts", destination: "hosts"
  config.vm.provision "file", source: "requirements.yml", destination: "requirements.yml"


  config.vm.define "ub1404" do |pentester|
    pentester.vm.box = "geerlingguy/ubuntu1204"
    #pentester.vm.box_version = "2021.01.04-0851"
    # pentester.vm.hostname = "tattoine"
    #pentester.ssh.username = 'vagrant'
    #pentester.ssh.password = 'vagrant'

    pentester.vbguest.auto_update = false
    pentester.ssh.insert_key = false
    pentester.ssh.connect_timeout = 20
    pentester.vm.boot_timeout = 120

    pentester.vm.network "private_network", ip: '10.55.56.52',
    	virtualbox__intnet: "metasploitable3",
    	nic_type: "virtio"

    pentester.vm.provider "virtualbox" do |v|
      v.name = ENV['boxname']
#      v.customize ["modifyvm", :id, "--description", File.read("Description")]
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
    config.vm.provision "shell", inline: <<-SHELL
    # ifconfig eth0 10.55.56.52 netmask 255.255.255.0 up
     tr -d '\r' < /vagrant/functions/ready >/usr/local/bin/ready && chmod 0700 /usr/local/bin/ready

     #/usr/local/bin/ready
     #/usr/local/bin/install_pkgs
     #/usr/local/bin/pull_repos
     #iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
     #iptables -A INPUT -p tcp --dport 3389 -m
   #config.vm.provision "shell", inline: <<-SHELL state --state NEW -j ACCEPT

    # setup_xrdp
    # setup_vnc
#    ls -l /home/vagrant
SHELL
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "/home/vagrant/playbook.yml"
    ansible.galaxy_role_file = "/home/vagrant/requirements.yml"
    inventory_path = "/home/vagrant/hosts"
  end
end
