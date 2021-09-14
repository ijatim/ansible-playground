# -*- mode: ruby -*-
# vi: set ft=ruby :

ubuntu = {
  "ubuntu-1" => "192.168.33.10",
  "ubuntu-2" => "192.168.33.11",
  "ubuntu-3" => "192.168.33.12"
}

centos = {
  "centos-1" => "192.168.33.20",
  "centos-2" => "192.168.33.21",
  "centos-3" => "192.168.33.22"
}

ubuntu_c = {
  "ubuntu-c" => "192.168.33.30"
}

Vagrant.configure("2") do |config|
  ubuntu_c.each do |name, ip|
    config.vm.define name do |machine|
      machine.vm.box = "ubuntu/bionic64"
      machine.vm.box_version = "20210831.0.0"
      machine.vm.hostname = "%s" % name
      machine.vm.network :private_network, ip: ip
      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--memory", 1024, "--cpus", 2, "--cpuexecutioncap", "50"]
      machine.vm.synced_folder "data/", "/vagrant"
      machine.vm.provision "shell", inline: "apt update && apt install sshpass -y && pip3 install virtualenv"
      machine.vm.provision "file", source: "/home/hamed/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/hamed-ubuntu.pub"
      machine.vm.provision "shell", inline: "cat /home/vagrant/.ssh/hamed-ubuntu.pub >> /home/vagrant/.ssh/authorized_keys"
      end
    end
  end
end


Vagrant.configure("2") do |config|
  centos.each do |name, ip|
    config.vm.define name do |machine|
      machine.vm.box = "centos/7"
      machine.vm.box_version = "2004.01"
      machine.vm.hostname = "%s" % name
      machine.vm.network :private_network, ip: ip
      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--memory", 256, "--cpus", 1, "--cpuexecutioncap", "30"]
      machine.vm.synced_folder "data/", "/vagrant"
      end
    end
  end
end

Vagrant.configure("2") do |config|
  config.vm.box_version = "20210831.0.0"
  ubuntu.each do |name, ip|
    config.vm.define name do |machine|
      machine.vm.box = "ubuntu/bionic64"
      machine.vm.box_version = "20210831.0.0"
      machine.vm.hostname = "%s" % name
      machine.vm.network :private_network, ip: ip
      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--memory", 256, "--cpus", 1, "--cpuexecutioncap", "50"]
      machine.vm.synced_folder "data/", "/vagrant"
      end
    end
  end
end
