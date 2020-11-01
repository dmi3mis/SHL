# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "opensuse/Leap-15.2.x86_64" 
  #config.vm.box = "generic/opensuse15"
  config.vagrant.plugins = [ "vagrant-timezone","vagrant-reload"]
  config.timezone.value = :host
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  
  config.vm.provider "virtualbox" do |vbox, override|
    # vbox.gui = true
    if ENV['VBOX_VM_PATH']
      vbox_vm_path = ENV['VBOX_VM_PATH']
    end
  end
  config.vm.provision :shell, path: "scripts/add-users"

  config.vm.define :"server1" do |server1_config|
    server1_config.vm.hostname = "server1.172.16.1.21.xip.io"
    server1_config.vm.network "private_network", ip: "172.16.1.21", auto_config: true
    server1_config.vm.network :forwarded_port, guest: 22, host: 6001, id: "ssh", host_ip: "127.0.0.1"
    # server1.vm.provision :shell, run: "always", inline: "yast2 lan edit id=0 bootproto='static' ip='172.16.1.21'"

    # server1_config.vbguest.installer_hooks[:before_install] = [ "zypper dup -y", "zypper in -y bzip2","zypper up -y kernel-default", "zypper in -y kernel-default-devel" ]
    server1_config.vm.provider "virtualbox" do |vbox, override|
      vbox.cpus   = 2
      vbox.memory = 4096
      vbox.name   = "server1.172.16.1.21.xip.io"
      #vbox.linked_clone = true
      #vbox.auto_nat_dns_proxy = false
      #vbox.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
      #vbox.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
      vbox.customize ["modifyvm", :id, "--ostype", "OpenSUSE_64" ]
      vbox.gui = true
      vbox.customize ["modifyvm", :id, "--usb", "on"]
      vbox.customize ["modifyvm", :id, "--usbehci", "on"]
      vbox.customize ["modifyvm", :id, "--vram", "32"]
      vbox.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vbox.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    server1_config.vm.provision  :shell, path: "scripts/add-users"
    server1_config.vm.provision  :shell, path: "scripts/add-dns"
    server1_config.vm.provision  "shell", inline: "zypper refresh && zypper update -y"
    server1_config.vm.provision  :reload
    server1_config.vm.provision "shell", inline: "zypper install -y -t pattern gnome && systemctl set-default graphical.target && systemctl isolate graphical.target && reboot"
  end
  
  
  config.vm.define :"server2" do |server2_config|
    server2_config.vm.hostname = "server2.172.16.1.22.xip.io"
    server2_config.vm.network "private_network", ip: "172.16.1.22", auto_config: true
    server2_config.vm.network :forwarded_port, guest: 22, host: 6002, id: "ssh", host_ip: "127.0.0.1"
    # server2.vm.provision :shell, run: "always", inline: "yast2 lan edit id=0 bootproto='static' ip='172.16.1.22'"
    # server2_config.vbguest.installer_hooks[:before_install] = [ "zypper dup -y", "zypper in -y bzip2","zypper up -y kernel-default", "zypper in -y kernel-default-devel"]
    server2_config.vm.provider "virtualbox" do |vbox, override|
      vbox.cpus   = 2
      vbox.memory = 4096
      vbox.name   = "server2.172.16.1.22.xip.io"
      #vbox.linked_clone = true
      #vbox.auto_nat_dns_proxy = false
      #vbox.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
      #vbox.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
#	    vbox.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', "2", '--device', "0", '--type', 'dvddrive', '--medium', vbox_dvd_path ]
#	    vbox.customize ["modifyvm", :id, "--boot1", "disk", "--boot2", "dvd"]

      vbox.customize ["modifyvm", :id, "--ostype", "OpenSUSE_64" ]
      vbox.gui = true
      vbox.customize ["modifyvm", :id, "--usb", "on"]
      vbox.customize ["modifyvm", :id, "--usbehci", "on"]
      vbox.customize ["modifyvm", :id, "--vram", "32"]
      vbox.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vbox.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end
    server2_config.vm.provision  :shell, path: "scripts/add-users"
    server2_config.vm.provision  :reload
    server2_config.vm.provision "shell", inline: "zypper refresh && zypper update -y && zypper install -y -t pattern gnome && systemctl set-default graphical.target && reboot"
	end
end
