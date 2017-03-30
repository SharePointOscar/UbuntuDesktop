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
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "boxcutter/ubuntu1604-desktop"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  #config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|

     # Display the VirtualBox GUI when booting the machine
     vb.gui = true

     # fixes an issue with terminal not firing up
     ENV['LC_ALL']="en_US.UTF-8"

     # Customize the amount of memory on the VM:
     vb.memory = "2024"

     # Enable, if Guest Additions are installed, whether hardware 3D acceleration should be available
     # if we enable this, Atom does not display correctly at startup, so disable for now.
     vb.customize ["modifyvm", :id, "--accelerate3d", "off"]

     vb.name = "Oscar's Desktop (@SharePointOscar)"
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    echo "Installing Git"
        apt-get install git -y > /dev/null
    echo "Installing yum"
        apt-get install yum -y > /dev/null
    echo "Installing Atom"
        sudo add-apt-repository ppa:webupd8team/atom -y > /dev/null
        sudo apt-get update
        sudo apt-get install atom
   SHELL

   # Terminal does not start if this is not set See: https://github.com/mitchellh/vagrant/issues/1188
   config.vm.provision "shell", inline: 'echo \'LC_ALL="en_US.UTF-8"\' > /etc/default/locale'

   # let's install Docker
   config.vm.provision :docker

   # Install docker-compose and docker-compose completion
   config.vm.provision "shell", inline: <<-EOC
     test -e /usr/local/bin/docker-compose || \\
     curl -sSL https://github.com/docker/compose/releases/download/1.5.1/docker-compose-`uname -s`-`uname -m` \\
       | sudo tee /usr/local/bin/docker-compose > /dev/null
     sudo chmod +x /usr/local/bin/docker-compose
     test -e /etc/bash_completion.d/docker-compose || \\
     curl -sSL https://raw.githubusercontent.com/docker/compose/$(docker-compose --version | awk 'NR==1{print $NF}')/contrib/completion/bash/docker-compose \\
       | sudo tee /etc/bash_completion.d/docker-compose > /dev/null

   EOC
end
