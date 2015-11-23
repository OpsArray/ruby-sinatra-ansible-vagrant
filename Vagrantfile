# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
ansible_tags = ENV['TAGS'] || 'all'
application_directory = ENV['APP_DIR']

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = true
  end

  # Vagrant Box information
  config.vm.box = "centos7"
  config.vm.box_url = "https://github.com/holms/vagrant-centos7-box/releases/download/7.1.1503.001/CentOS-7.1.1503-x86_64-netboot.box"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  # Virtualbox provider information
  config.vm.provider :virtualbox do |vb|
    vb.name = "sinatra"
    vb.memory = 512
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Networking
  config.vm.hostname = "sinatra"
  config.vm.network :private_network, ip: "192.168.56.102"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :sinatra do |sinatra|
  end

  if application_directory != nil
    config.vm.synced_folder "#{application_directory}", "/var/www/html/production", :mount_options => [ 'dmode=775', 'fmode=775']
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "inventory"
    ansible.limit = "app"
    ansible.tags = "#{ansible_tags}"
    # Having trouble? Uncomment below to troubleshoot.
    # ansible.verbose = "vvvv"
  end

end
