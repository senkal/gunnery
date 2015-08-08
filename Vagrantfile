# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("1") do |config|
  config.vm.box = "ubuntu/trusty32"

  config.vm.host_name = "void"
#  config.vm.network :bridged

  config.vm.forward_port 80, 8080
  config.vm.forward_port 8080, 8081
  config.vm.forward_port 5432, 5432
  config.ssh.forward_agent = true

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "puppet/manifests"
    puppet.module_path = "puppet/modules"
    puppet.manifest_file = "base.pp"
    puppet.options = "--hiera_config /vagrant/puppet/manifests/hiera.yaml"
    puppet.facter = {
        "environment" => "development",
    }
  end
end

Vagrant.configure("2") do |config|
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", 356]
    vb.customize ["modifyvm", :id, "--ioapic", "Off"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end
end
