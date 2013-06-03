# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Use Ubuntu 12.04 LTS x64, for larger MongoDB database support
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Hostname and Synced Folder for Vagrant 1.2
  config.vm.hostname = "devbox"
  # Neither 777 nor setting web root owner to www-data are safe in production environment, this is only to workaround virtualbox limits
  config.vm.synced_folder "www", "/var/www", :extra => "dmode=777,fmode=777", :owner => "vagrant", :group => "vagrant"

  # Basic private network for Vagrant 1.2
  config.vm.network :private_network, ip: "192.168.10.10"

  # Set a local time
  config.vm.provision :shell, :inline => "echo \"Asia/Hong_Kong\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  # Puppet will handle the rest of install
  config.vm.provision :puppet do |puppet|
     puppet.facter = { "fqdn" => "local.devbox", "hostname" => "devbox" }
     puppet.manifests_path = "manifests"
     puppet.manifest_file  = "base.pp"
     puppet.module_path = "modules"
  end

  # Skip guest addition check, this base already has guest addition installed
  config.vbguest.auto_update = false

end
