# -*- mode: ruby -*-
# vi: set ft=ruby :

# Boostrap Script
$script = <<SCRIPT

sed -i 's/us.archive/de.archive/g' /etc/apt/sources.list
add-apt-repository ppa:octave/stable

# Update & Install
apt-get update
apt-get install -y octave gnuplot xauth

echo "cd /vagrant" >> /home/vagrant/.bashrc

SCRIPT

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  #config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # A Vagrant plugin that helps you reduce the amount of coffee you drink while
  # waiting for boxes to be provisioned by sharing a common package cache among
  # similiar VM instances. Kinda like vagrant-apt_cache or this magical snippet
  # but targetting multiple package managers and Linux distros.
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.auto_detect = true

    # For VirtualBox, we want to enable NFS for shared folders
    # config.cache.enable_nfs = true
  end

  # The shell provisioner allows you to upload and execute a script as the root
  # user within the guest machine.
  config.vm.provision :shell, :inline => $script

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "256", "--cpus", "2"]
  end

  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true
end
