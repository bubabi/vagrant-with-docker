Vagrant.configure(2) do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  
  # an alternative to this Ubuntu 14.04 box is the "v0rtex/xenial64" with the 16.04 LTS
  
  # access a port on your host machine (via localhost) and 
  # have all data forwarded to a port on the guest machine.  
  
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.

  #define a larger than default (40GB) disksize
  config.vm.box = "ubuntu/trusty64" 
  config.vm.network "forwarded_port", guest: 2375, host: 2375
  config.disksize.size = '50GB'
  
  config.vm.provider "virtualbox" do |vb|
    vb.name = 'build_machine'
    vb.memory = 4096
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  # set up Docker in the new VM:
  config.vm.provision "docker"
  
  config.vm.provision "file", source: "\daemon.json", destination: "/tmp/daemon.json"
  
  $script = <<-SCRIPT
  sudo su
  mv /tmp/daemon.json /etc/docker/daemon.json
  SCRIPT

  config.vm.provision "shell", inline: $script


end
