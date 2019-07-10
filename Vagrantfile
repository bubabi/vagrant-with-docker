Vagrant.configure("2") do |config|
  config.vm.box = "alpine/alpine64"
  config.vm.box_version = "3.6.0"
  config.vm.network "forwarded_port", guest: 2375, host: 2375

  config.vm.provider "virtualbox" do |vb|
    vb.name = 'build_box'
    vb.memory = "1024"
    vb.cpus = "2"
	vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end
  
  config.vm.provision "file", source: "\daemon.json", destination: "/tmp/daemon.json"
  
  config.vm.provision "shell", inline: <<-SHELL
    echo http://dl-cdn.alpinelinux.org/alpine/v3.6/community >> /etc/apk/repositories
    apk update
    apk add docker='17.05.0-r0'
    rc-update add docker boot
    sudo su
    echo $PWD
    var=$(ls /tmp/)
    echo $var
    mkdir /etc/docker
    var2=$(ls /etc/)
    echo $var2
    mv /tmp/daemon.json /etc/docker/daemon.json
    service docker restart
  SHELL
  
end
