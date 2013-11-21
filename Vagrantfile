MEMORY_MB = '2048'

Vagrant.configure("2") do |config|
    config.vm.box = "precise64"

    config.vm.provider :virtualbox do |vb|
        config.vm.box_url = "http://files.vagrantup.com/precise64.box"
        config.vm.network :private_network, ip: "192.168.10.2"
        vb.customize ["modifyvm", :id, "--memory", MEMORY_MB]
    end

    config.vm.provider :vmware_fusion do |v|
        config.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
        config.vm.network :private_network, ip: "192.168.11.2"
        v.vmx["memsize"] = MEMORY_MB 
        v.vmx["vhv.enable"] = "TRUE"
    end

    config.vm.provision :shell,
                        inline: "cd /vagrant && FORCE_PREREQ=1 ./stack.sh",
                        privileged: false
end
