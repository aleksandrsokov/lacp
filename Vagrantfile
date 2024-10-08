# -*- mode: ruby -*-
# vim: set ft=ruby :

Vagrant.configure(2) do |config|

    config.vm.provider "virtualbox" do |v|
      v.memory = 1280
      v.cpus = 2
    end
    
    config.vm.define "inetRouter" do |inetRouter|
      inetRouter.vm.box = "centos/stream9"
      inetRouter.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "router-net"
      inetRouter.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "router-net"
      inetRouter.vm.network "private_network", ip: '192.168.56.10', adapter: 8
      inetRouter.vm.hostname = "inetRouter"
    
#      inetRouter.vm.provision "shell", inline: <<-SHELL
#        mkdir -p ~root/.ssh
#        cp ~vagrant/.ssh/auth* ~root/.ssh
#        systemctl restart sshd
#       SHELL
    end

    config.vm.define "centralRouter" do |centralRouter|
      centralRouter.vm.box = "centos/stream9"
      centralRouter.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "router-net"
      centralRouter.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "router-net"
      centralRouter.vm.network "private_network", ip: '192.168.255.9', adapter: 6, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"
      centralRouter.vm.network "private_network", ip: '192.168.56.11', adapter: 8
      centralRouter.vm.hostname = "centralRouter"
        
#      centralRouter.vm.provision "shell", inline: <<-SHELL
#        mkdir -p ~root/.ssh
#        cp ~vagrant/.ssh/auth* ~root/.ssh
#        systemctl restart sshd
#        SHELL
    end

    config.vm.define "office1Router" do |office1Router|
        office1Router.vm.box = "centos/stream9"
        office1Router.vm.network "private_network", ip: '192.168.255.10', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"
        office1Router.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "vlan1"
        office1Router.vm.network "private_network", adapter: 4, auto_config: false, virtualbox__intnet: "vlan1"
        office1Router.vm.network "private_network", adapter: 5, auto_config: false, virtualbox__intnet: "vlan2"
        office1Router.vm.network "private_network", adapter: 6, auto_config: false, virtualbox__intnet: "vlan2"
        office1Router.vm.network "private_network", ip: '192.168.56.20', adapter: 8
        office1Router.vm.hostname = "office1Router"
          
#       office1Router.vm.provision "shell", inline: <<-SHELL
#         mkdir -p ~root/.ssh
#         cp ~vagrant/.ssh/auth* ~root/.ssh
#         systemctl restart sshd
#         SHELL
      end

      config.vm.define "testClient1" do |testClient1|
        testClient1.vm.box = "centos/stream9"
        testClient1.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        testClient1.vm.network "private_network", ip: '192.168.56.21', adapter: 8
        testClient1.vm.hostname = "testClient1"
          
#        testClient1.vm.provision "shell", inline: <<-SHELL
#          mkdir -p ~root/.ssh
#          cp ~vagrant/.ssh/auth* ~root/.ssh
#          systemctl restart sshd
#          SHELL
      end

      config.vm.define "testServer1" do |testServer1|
        testServer1.vm.box = "centos/stream9"
        testServer1.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        testServer1.vm.network "private_network", ip: '192.168.56.22', adapter: 8
        testServer1.vm.hostname = "testServer1"
          
#        testServer1.vm.provision "shell", inline: <<-SHELL
#          mkdir -p ~root/.ssh
#          cp ~vagrant/.ssh/auth* ~root/.ssh
#          systemctl restart sshd
#          SHELL
      end

      config.vm.define "testClient2" do |testClient2|
        testClient2.vm.box = "ubuntu/jammy64"
        testClient2.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        testClient2.vm.network "private_network", ip: '192.168.56.31', adapter: 8
        testClient2.vm.hostname = "testClient2"
          
        testClient2.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          systemctl restart sshd
          SHELL
      end

      config.vm.define "testServer2" do |testServer2|
        testServer2.vm.box = "ubuntu/jammy64"
        testServer2.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        testServer2.vm.network "private_network", ip: '192.168.56.32', adapter: 8
        testServer2.vm.hostname = "testServer2"
          
        testServer2.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          systemctl restart sshd
          SHELL

        testServer2.vm.provision "ansible" do |ansible|
          ansible.playbook = "ansible/provision.yml"
          #ansible.inventory_path = "ansible/hosts"
          #ansible.host_key_checking = "false"
          ansible.become = "true"
          ansible.limit = "all"
       end
      end

end