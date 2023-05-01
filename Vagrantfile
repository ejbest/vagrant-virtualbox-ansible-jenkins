# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"
  config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.boot_timeout = 1500

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  config.vm.synced_folder "./ansible", "/ansible"

  config.vm.provision "shell", inline: <<-SHELL
    apt update && \
    apt install -y python3 python3-pip && \
    pip3 install setuptools-rust && \
    CRYPTOGRAPHY_DONT_BUILD_RUST=1 pip3 install -U pip ansible && \
    ansible-playbook /ansible/playbook.yml
  SHELL

  config.vm.provider 'virtualbox' do |vb|
    vb.customize ['modifyvm', :id, '--cableconnected1', 'on']
  end
  config.vm.provider 'virtualbox' do |vb|
    vb.customize ['modifyvm', :id, '--cableconnected1', 'on']
  end
end
