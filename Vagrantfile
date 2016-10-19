# -*- mode: ruby -*-
# vi: set ft=ruby :

# rails5のローカル開発環境作成用Vagrantfile
# @see https://atlas.hashicorp.com/centos/boxes/7
# @author keita-nishimoto
# @since 2016-10-19
Vagrant.configure(2) do |config|
  config.ssh.insert_key = false
  config.vm.box = "centos/7"
  config.vm.network "private_network", ip: "192.168.33.50"
  config.vm.provider "virtualbox" do |vm|
    vm.customize ["modifyvm", :id, "--memory", "1024", "--cpus", "2", "--ioapic", "on"]
  end

  %w(
    rails5-api-prototype
  ).each do |dir|
    config.vm.synced_folder "../#{dir}", "/home/vagrant/#{dir}", mount_options: ["dmode=777","fmode=777"] if  File.exist?("../#{dir}")
  end

  config.vm.provision "ansible" do |ansible|
    ansible.limit = "all"
    ansible.inventory_path = "../rails5-ansible/local"
    ansible.playbook = "../rails5-ansible/site.yml"
  end
end
