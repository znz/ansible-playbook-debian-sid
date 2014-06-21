# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = ENV["VM_HOSTNAME"] || "debian-sid"
  config.vm.box = 'debian-73-x64-virtualbox-nocm'
  config.vm.box_url = 'http://puppet-vagrant-boxes.puppetlabs.com/debian-73-x64-virtualbox-nocm.box'

  #config.vm.network :forwarded_port, guest: 80, host: 3080

  config.vm.provider "virtualbox" do |vb|
    # Don't boot with headless mode
    vb.gui = true if ENV["VM_GUI"]

    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", ENV["VM_MEMORY"] || "512"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.verbose = ENV["ANSIBLE_VERBOSE"] if ENV["ANSIBLE_VERBOSE"]
    ansible.tags = ENV["ANSIBLE_TAGS"] if ENV["ANSIBLE_TAGS"]
  end
end
