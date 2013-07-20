Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.hostname = 'apdl.dev'
  config.vm.network :private_network, ip: "192.168.33.11"

  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--name", "apdl-master"]
  end

  config.vm.synced_folder "./htdocs", "/var/www", id: "htdocs"

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "env/manifests"
    puppet.module_path = "env/modules"
    puppet.options = ['--verbose']
  end

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

end
