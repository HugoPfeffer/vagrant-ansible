
Vagrant.configure("2") do |config|

    config.vm.synced_folder ".", "/home/vagrant/shared-host"
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  
    config.vm.define 'centos' do |master|
      master.vm.box = "generic/centos8"
      master.vm.provider "virtualbox" do |v|
        v.memory = 1024
      end

      master.vm.provision "shell", inline: "echo alias clearkhosts='> /home/vagrant/.ssh/known_hosts' >> /home/vagrant/.bashrc" 
      master.vm.provision "shell", inline: "echo alias vagrant_pkey='cp shared-host/.vagrant/machines/wordpress/virtualbox/private_key /home/vagrant/' >> /home/vagrant/.bashrc" 
      master.vm.provision "shell", inline: "yum install -y epel-release && yum install -y ansible" 
      master.vm.network "private_network", ip: "172.17.177.39"
      master.vm.hostname = 'centos.local'
    end
  
    
    config.vm.define "wordpress" do |node1|
      node1.vm.box = "ubuntu/trusty64"
      node1.vm.network "private_network", ip: "172.17.177.40"
    end
    config.vm.define "mysql" do |node2|
      node2.vm.box = "ubuntu/trusty64"
      node2.vm.network "private_network", ip: "172.17.177.42"
    end
  
  end