# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. # Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
    config.vm.box = 'ubuntu/bionic64'

    superlists_port = 50776
    config.vm.network "forwarded_port", guest: 80, host: superlists_port
    config.vm.network "forwarded_port", guest: 8000, host: 50777

    config.vm.hostname = 'guest'

    config.vm.synced_folder "../", "/vagrant"

    config.vm.provider :virtualbox do |vb|
       vb.gui = true
    end

    config.vm.provision 'shell', inline: <<-SHELL
         sudo apt-get --assume-yes install python
    SHELL

    config.vm.provision 'ansible' do |ansible|

        ansible.limit = 'development'
        ansible.inventory_path = 'hosts'

        ansible.playbook = 'site.yml'

        # Debug
        #ansible.verbose = 'vvvv'

    end

end