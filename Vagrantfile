ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'
Vagrant.configure("2") do |config|
    config.vm.define "ns01" do |ns01|
        ns01.vm.box = 'bento/ubuntu-24.04'
        ns01.vm.host_name = 'ns01'
        ns01.vm.network :forwarded_port, host: 2301, guest: 22        
        ns01.vm.network :private_network, ip: "192.168.60.10", virtualbox__intnet: 'dns', adapter: 2
        ns01.vm.provider "virtualbox" do |vb|
            vb.memory = 1024            
        end
        
        ns01.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_ns01/provision.yml"
            ansible.inventory_path = "ansible_ns01/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "ns02" do |ns02|
        ns02.vm.box = 'bento/ubuntu-24.04'
        ns02.vm.host_name = 'ns02'
        ns02.vm.network :forwarded_port, host: 2302, guest: 22        
        ns02.vm.network :private_network, ip: "192.168.60.11", virtualbox__intnet: 'dns', adapter: 2
        ns02.vm.provider "virtualbox" do |vb|
            vb.memory = 1024            
        end
        
        ns02.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_ns02/provision.yml"
            ansible.inventory_path = "ansible_ns02/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end


    config.vm.define "client1" do |client1|
        client1.vm.box = 'bento/ubuntu-24.04'
        client1.vm.host_name = 'client1'
        client1.vm.network :forwarded_port, host: 2303, guest: 22        
        client1.vm.network :private_network, ip: "192.168.60.15", virtualbox__intnet: 'dns', adapter: 2
        client1.vm.provider "virtualbox" do |vb|
            vb.memory = 1024            
        end
        
        client1.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_client1/provision.yml"
            ansible.inventory_path = "ansible_client1/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "client2" do |client2|
        client2.vm.box = 'bento/ubuntu-24.04'
        client2.vm.host_name = 'client2'
        client2.vm.network :forwarded_port, host: 2304, guest: 22        
        client2.vm.network :private_network, ip: "192.168.60.16", virtualbox__intnet: 'dns', adapter: 2
        client2.vm.provider "virtualbox" do |vb|
            vb.memory = 1024            
        end
        
        client2.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_client2/provision.yml"
            ansible.inventory_path = "ansible_client2/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end
end