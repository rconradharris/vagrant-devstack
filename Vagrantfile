# 1024 doesn't seem to be enough, system becomes non-reponsive and
# load-average goes very high (35+).
MEMORY_MB = '2048'

Vagrant.configure("2") do |config|
    config.vm.box = "precise64"
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"
    config.vm.network :private_network, ip: "192.168.11.2"

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", MEMORY_MB]
    end

    config.vm.provider :vmware_fusion do |v, override|
        override.vm.box = "precise64_fusion"
        override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"

        v.vmx["memsize"] = MEMORY_MB 

        # Enable Intel VT-x/EPT virtualization in VM so we can boot guests
        v.vmx["vhv.enable"] = "TRUE"
    end

    config.vm.provision :shell,
                        inline: "cd /vagrant && FORCE_PREREQ=1 ./stack.sh",
                        privileged: false
end
