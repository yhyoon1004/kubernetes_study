# Vagrant

>1. Vagrant 란?
>2. 사용법


## 1. Vagrant 란?
가상 머신을 쉽게 만들고 관리해주는 도구  
가상머신은 VirtualBox 같은 소프트웨어가 생성하는 데  
Vagrant 생성과정이나 관리를 편리하게 해주는 도구  
코드로 가상 머신을 구성할 수 있다.

## 2. 사용법

---
**기본 용어**
- box : Vagrant 환경구성 묶음
  - `https://portal.cloud.hashicorp.com/vagrant/discover`   
    여기서 provider에 맞게 필요한 박스 정보를 찾아 설치
- provider : 가상화 가능 제공 소프트웨어 (VirtualBox, Hyper-V, Docker)

---
**기본 명령어**
- `vagrant box list` :  현재 다운받은 box 목록 조회
- `vagrant box add 이름` : 해당 이름의 box를 다운로드
  - ex)  `vagrant box add bento/ubuntu-16.04`
- `vagrant box remove 이름` : 해당 이름의 box 삭제
  - ex) `vagrant box remove bento/ubuntu-16.04`
- `vagrant init bento/ubuntu-16.04` : 해당 박스로 vagrant 환경 초기화
- `vagrant up` : 현재 위치한 vagrant 환경을 기준으로 가상 머신 생성
- `vagrant ssh` : 현재 위치에 생성한 가상머신에 ssh 연결
- `vagrant halt` :  가상 머신 중지
- `vagrant reload` : 가상 머신 재시작
- `vagrant destroy` : 가상 머신 삭제

---
- `vagrant init bento/ubuntu-16.04` 명령 실행시 생성되는 `Vagrantfile`의 내용.  
주석 친부분을 자세히 보면 자원할당 설정이 있는 것을 볼 수있는 데  
필요하다면 해당 주석을 지우거나 내용을 추가하여 실행하면 됨.
````
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "bento/ubuntu-16.04"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end

````
  

- 설정 추가 예시  
```
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"  # 사용할 OS 설정
  config.vm.network "private_network", type: "dhcp"  # 네트워크 설정
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  # RAM 1GB 설정
    vb.cpus = 2         # CPU 2개 설정
  end
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update -y
    apt-get install -y nginx
  SHELL
end
```
