$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love Linux"
touch file1
SCRIPT
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Example for VirtualBox:
  #
    config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  # Customize the amount of memory on the VM:
      vb.memory = "1024"
    end
  #configure provisioners on tha machine
    config.vm.provision :docker
    config.vm.provision :shell, path: "bootstrap.sh"
    config.vm.provision :file, source: "newfile", destination: "newfile"
    config.vm.provision :file, source: "HTML", destination: "HTMLDIR"

    config.vm.define "server-1" do |dockerserver|
      dockerserver.vm.network "private_network", ip: '192.168.56.60'
      dockerserver.vm.hostname = "dockerserver"
      dockerserver.vm.provision :shell, inline: "echo Hi Class!"
      dockerserver.vm.provision "shell", inline: $script
      dockerserver.vm.provision "shell" do |s|
        s.inline = "echo $1"
        s.args = ["AT", "Class!"]
      end
      dockerserver.vm.provision "docker" do |d|
        d.run "hello-world"
      end
    end
end
