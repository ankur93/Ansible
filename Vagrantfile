# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|  
  config.ssh.forward_agent = true
  config.vm.define "ppe1" do |ppe|
    ppe.vm.box = "centos/7"
    ppe.vm.hostname = 'ppe1'

    ppe.vm.network :private_network, ip: "192.167.56.101"
    #ppe.vm.network :forwarded_port, guest: 22, host: 10122, id: "ssh"
    ppe.ssh.forward_agent = true
    ppe.ssh.insert_key = false
    ppe.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
    ppe.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"

    ppe.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
    end

    ppe.vm.provision "shell", inline: <<-SHELL
      sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
      sudo systemctl restart sshd.service
      echo "finished"
      yum install -y epel-release
      yum install -y ansible nc net-tools
    SHELL
  end

  config.vm.define "ppe2" do |ppe|
    ppe.vm.box = "centos/7"
    ppe.vm.hostname = 'ppe2'

    ppe.vm.network :private_network, ip: "192.167.56.102"
    #ppe.vm.network :forwarded_port, guest: 22, host: 10222, id: "ssh"

    ppe.ssh.insert_key = false
    ppe.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
    ppe.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"

    ppe.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
    end

    ppe.vm.provision "shell", inline: <<-SHELL
      sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
      sudo systemctl restart sshd.service
      echo "finished"
      yum install -y epel-release
      yum install -y ansible nc net-tools
    SHELL
  end
end
