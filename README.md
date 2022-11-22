# vagrant-box-devops

A simple Vagrantfile to setup a development environment based on Ubuntu desktop with some DevOps toolset in it.

## Requisites

For running this box, you need to have the following tools:

- VirtualBox
- Vagrant

💡 Pro tip

On Windows, you can install both at once with Chocolatey with

```
choco install virtualbox vagrant
```

## Toolset

- Docker and docker-compose
- Python 3.10
- Git
- Ansible 2.13
- Google Chrome

## How to use?

For SSH access, public key on the host machine `~/.ssh/id_rsa.pub` is added to the `authorized_keys` file of the vagrant box. You have a different key? Simply change the file path in `Vagrantfile`.

```
vagrant up

vagrant ssh
```

Username / Password for remote desktop connection: `vagrant / vagrant`
