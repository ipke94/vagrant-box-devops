# Install plugins before
# vagrant plugin install vagrant-docker-compose

Vagrant.configure("2") do |config|

  config.vm.box = "generic/ubuntu2204"

  config.vm.provider :virtualbox do |v|
    v.name = 'ubuntu2204-custom-desktop-vm'
    #v.memory = 8192
    #v.cpus = 2
    v.customize ['modifyvm', :id, '--graphicscontroller', 'vmsvga']
    v.customize ['modifyvm', :id, '--vram', '16']
    v.customize ["modifyvm", :id, "--clipboard-mode", "bidirectional"]
    v.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
    v.gui = true
  end

  config.vm.network "private_network", ip: "192.168.56.20"
  config.vm.synced_folder "./sharedfolder", "/mnt/sharedfolder", type: "virtualbox", automount: true
  config.vm.provision :docker
  config.vm.provision :docker_compose
  # Copy ssh keypair and config files to the guest machine
  config.vm.provision "file", source: "~/.ssh/.", destination: "~/.ssh"

  config.vm.provision "shell", inline: <<-SHELL
    # Update package index
    apt update -y
    # Upgrade packages
    apt-get upgrade -y
	  
    # Install toolset
    apt install -y ubuntu-desktop
    apt install -y python3-pip python3-venv
    # ansible and linters
    apt install software-properties-common
    apt-add-repository --yes --upadte ppa:ansible/ansible
    apt install -y ansible yamllint
    pip3 install ansible-lint
	
    # Configure vm
    timedatectl set-timezone Europe/Amsterdam
    cat /home/vagrant/.ssh/*.pub >> /home/vagrant/.ssh/authorized_keys
    # Install Chrome
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
    dpkg -i google-chrome-stable_current_amd64.deb
  SHELL
end
