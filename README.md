# vagrant-box-devops

A simple Vagrantfile to setup a development environment based on Ubuntu desktop
with some generic DevOps toolset in it.

## Requisites

To run this box, you need the following tools:

- VirtualBox
- Vagrant

💡 Pro tip

On Windows, you can install both at once with Chocolatey:

```
choco install virtualbox vagrant
```

## Tools in the box

- docker and docker-compose
- python3, pip
- git
- ansible
- ansible-lint, yamllint
- google chrome

## How to use?

For SSH access, all sile in `~/.ssh` are copied to the home of vagrant user
also public keys are added to `authorized_keys`.

```bash
# Install required plugin
vagrant plugin install vagrant-docker-compose

# Start up / provision the VM
vagrant up

# Connect with SSH
vagrant ssh
# or
# ssh -i ~/.ssh/id_rsa vagrant@192.168.56.20
```

Username / Password for remote desktop connection: `vagrant / vagrant`
