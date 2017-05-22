
basebox = "bento/ubuntu-16.04"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.define :controller do |controller_config|
        controller_config.vm.box = basebox
        controller_config.vm.host_name = "controller.example.com"
        controller_config.vm.network :private_network, ip:"192.168.100.10"
        controller_config.vm.network :private_network, ip:"192.168.200.10"
		config.vm.provider :virtualbox do |vb|
		    vb.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
            vb.customize ["modifyvm", :id, "--memory", "8000"]
            vb.customize ["modifyvm", :id, "--cpus", "4"]
        end
        controller_config.vm.provision "shell", privileged: false, path: "devstack1.sh"
        controller_config.vm.provision "file", source: "local.conf.controller",
            destination: "~/devstack/local.conf"
        controller_config.vm.provision "shell", privileged: false, path: "devstack2.sh"
    end

    config.vm.define :compute1 do |compute1_config|
        compute1_config.vm.box = basebox
        compute1_config.vm.host_name = "compute1.example.com"
        compute1_config.vm.network :private_network, ip:"192.168.100.30"
        compute1_config.vm.network :private_network, ip:"192.168.200.30"
        config.vm.provider :virtualbox do |vb|
		    vb.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
            vb.customize ["modifyvm", :id, "--memory", "2000"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
        end
        compute1_config.vm.provision "shell", privileged: false, path: "devstack1.sh"
        compute1_config.vm.provision "file", source: "local.conf.compute",
            destination: "~/devstack/local.conf"
        compute1_config.vm.provision "shell", privileged: false, path: "devstack2.sh"
    end

end
