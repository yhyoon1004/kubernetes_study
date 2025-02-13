# Component 동작으로 이해하기

```shell
Vagrant.configure("2") do |config| 
    # Control Plane과 Worker Node가 동시에 구축된 기존의 VM 
    config.vm.define "docker" do |centos|
    config.vm.boot_timeout = 1800
        centos.vm.box = "ubuntu/focal64"
        centos.vm.hostname = "docker"
        centos.vm.network "private_network", ip: "192.168.100.100"
        centos.vm.provider "virtualbox" do |vb|
            vb.name = "docker"
            vb.cpus = 2
            vb.memory = 4096    
        end
    end

    # Worker Node로 구성할 새로운 VM
    config.vm.define "worker" do |centos|
    config.vm.boot_timeout = 1800
        centos.vm.box = "ubuntu/focal64"
        centos.vm.hostname = "worker"
        centos.vm.network "private_network", ip: "192.168.100.101"
        centos.vm.provider "virtualbox" do |vb|
            vb.name = "worker"
            vb.cpus = 2
            vb.memory = 4096    
        end
    end
end
```