# Install plugins before
# vagrant plugin install vagrant-docker-compose

Vagrant.configure("2") do |config|

  config.vm.box = "generic/ubuntu2204"

  config.vm.provider :virtualbox do |v|
    v.name = 'ubuntu2204-custom-desktop-vm'
    v.memory = 8192
    v.cpus = 2
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
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/me.pub"

  config.vm.provision "shell", inline: <<-SHELL
    # Add PPA for ansible
	apt-add-repository ppa:ansible/ansible
	# Update package index
    apt-get update -y
    # Upgrade installed packages
    apt-get upgrade -y
    
	# Install tools with package manager
    apt install -y ubuntu-desktop
    apt install -y python3-pip python3-venv
    apt install -y ansible
	
	# Install Poetry
	curl -sSL https://install.python-poetry.org | python3 -
	echo 'export PATH="/home/vagrant/.local/bin:$PATH"' >> /home/vagrant/.bashrc
    
	# Configure vm
    timedatectl set-timezone Europe/Amsterdam
	cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
    
	# Install Chrome
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
    dpkg -i google-chrome-stable_current_amd64.deb
  SHELL
end
