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
  config.vm.box = "generic/rhel8"
  config.vm.box_version = "~>3.6.0"

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
  config.vm.provider "hyperv" do |hp| 
    hp.maxmemory = 8196
    hp.vmname = "earthenterprise"
    hp.enable_virtualization_extensions = true
    hp.linked_clone = true
    end

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

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
  if Vagrant.has_plugin?('vagrant-registration')
    config.registration.username = ENV['VAGRANT_CONFIG_REDHAT_USERNAME']
    config.registration.password = ENV['VAGRANT_CONFIG_REDHAT_PASSWORD']
  end

  config.vm.synced_folder "./", "/earthenterprise/"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    dnf install -y gcc gcc-c++ kernel-devel libtirpc-devel
    dnf install -y bzip2 rsync perl perl-Perl4-CoreLibs
    dnf install -y python2 python2-devel
    dnf install -y doxygen zlib-devel libxml2-devel geos-devel proj-devel pcre-devel expat-devel libjpeg-turbo-devel giflib-devel libpng-devel glib2-devel libicu-devel libX11-devel pulseaudio-libs-devel libXext-devel libXcursor-devel libXrandr-devel fontconfig-devel libXinerama-devel libSM-devel libmng-devel mesa-libGL-devel xerces-c-devel boost libcap-devel openjpeg2-devel gtest-devel
    find /usr/lib64 -maxdepth 1 -regex '^.*libboost.*so.+' | sed 's/\(^.*libboost.*so\)\(.*\)/mv & \1/' | sudo sh
    sudo pip2 install -Iv scons==3.1.2 GitPython
    dnf install -y git git-lfs
  SHELL
end
