# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  #config.vm.hostname = "cookbook-joomla"
  config.vm.box = "precise64"
  #config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  #config.vm.network :private_network, ip: "33.33.33.10"
  #config.omnibus.chef_version = "11.6.0"
  #config.berkshelf.enabled = true
  #config.vm.network :hostonly, "192.168.33.10"


  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  config.vm.forward_port 80, 8082
  config.vm.forward_port 443, 8081

  config.vm.provision :chef_solo do |chef|
    chef.log_level = :debug
    chef.json = {
      :mysql => {
        :server_root_password => 'rootpass',
        :server_debian_password => 'debpass',
        :server_repl_password => 'replpass'
      },
      :joomla => {
        :db => {
          :pass => "joomT3st"
        }
      }
    }
    chef.run_list = [
      "recipe[apt]",
      "recipe[joomla::mysql]",
      "recipe[joomla::default]",
    ]
  end
end
