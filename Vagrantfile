# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|
  config.vm.box = "bento/ubuntu-20.04"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. 
  config.vm.network "forwarded_port", guest: 80, host: 8089
  config.vm.network "forwarded_port", guest: 443, host: 8449
  config.vm.network "forwarded_port", guest: 8080, host: 8009

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.56.200", :adapter => 2

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "~/vagrant-data", "/vagrant-data", create: true
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     # vb.gui = true
     vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "8096"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.
  config.ssh.forward_agent    = true
  config.ssh.insert_key       = true

  Vagrant.configure("2") do |config|
  config.vm.provision "shell",
    inline: "sudo apt-get update; sudo apt-get install -y git make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev python3-pip"
  end
end
