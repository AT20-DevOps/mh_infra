
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"

  # Example for VirtualBox:
    config.vm.provider "virtualbox" do |vb|
  # Customize the amount of memory on the VM:
      vb.memory = "1024"
    end
  #configure provisioners on tha machine
    config.vm.provision :docker
    config.vm.provision :docker_compose

    config.vm.define "ci-server" do |ciserver|
      ciserver.vm.network "private_network", ip: '192.168.56.61'
      ciserver.vm.hostname = "ci-server"
    end

    config.vm.define "server-2" do |server2|
      server2.vm.network "private_network", ip: '192.168.56.70'
      server2.vm.hostname = "server-2"
      server2.vm.provision :file, source: "AT20_CONVERT_SERVICE", destination: "AT20_CONVERT_SERVICE"
      server2.vm.provision :file, source: "docker-compose.yaml", destination: "docker-compose.yaml"
      server2.vm.provision :file, source: ".env", destination: ".env"
    end
end
