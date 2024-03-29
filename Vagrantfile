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
  config.vm.box = "ubuntu/bionic64"
  #Pinned to a specific version to prevent any breaks when updates
  #to the base image above
  config.vm.box_version = "~> 20200304.0.0"

  #maps a port from the local(host) machine(i.e my com) to the development
  #server(guest)
  config.vm.network "forwarded_port", guest: 8000, host: 8000

  config.vm.provision "shell", inline: <<-SHELL
  # First 2 lines disable to auto-update which will conflict with the sudo apt-get update
    systemctl disable apt-daily.service
    systemctl disable apt-daily.timer
  
    sudo apt-get update

    #server gets updated so that python3 virtual environment
    #and zip tool gets installed
    sudo apt-get install -y python3-venv zip

    #create a bash alias file and set python3 as the default python
    #everytime servers run, uses pyhton 3 as default so we dont need to write python3 everytime
    # Make sure it starts with /vagrant -> all project files
    # will be located here
    touch /vagrant/.bash_aliases
    if ! grep -q PYTHON_ALIAS_ADDED /home/vagrant/.bash_aliases; then
      echo "# PYTHON_ALIAS_ADDED" >> /home/vagrant/.bash_aliases
      echo "alias python='python3'" >> /home/vagrant/.bash_aliases
    fi
  SHELL
 end
