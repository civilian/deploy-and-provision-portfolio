# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. # Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
    config.vm.box = 'ubuntu/bionic64'

    ssh_port = 50777
    config.vm.network "forwarded_port", guest: 22, host: ssh_port, id: 'ssh'

    tdd_django_ottg_port = 50778
    config.vm.network "forwarded_port", guest: tdd_django_ottg_port, host: tdd_django_ottg_port

    blog_django_port = 50779
    config.vm.network "forwarded_port", guest: blog_django_port, host: blog_django_port

    config.vm.hostname = 'guest'

    config.vm.synced_folder ".", "/vagrant"

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
