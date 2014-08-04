
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu14"

  config.vm.define :webserver do |webserver|
    # For Jenkins
    webserver.vm.network "forwarded_port", guest: 8080, host: 8181
    webserver.vm.hostname = "webserver"
    webserver.vm.network "private_network", ip: "10.1.2.14"
    webserver.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible-ci/webserver.yml"
    end
  end

  config.vm.define :master do |master|
    # For Jenkins
    master.vm.network "forwarded_port", guest: 8080, host: 8282
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "10.1.2.15"
    master.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible-ci/jenkins-master.yml"
    end
  end

  config.vm.define :slave do |slave|
    slave.vm.hostname = "slave"
    slave.vm.network "private_network", ip: "10.1.2.16"
    slave.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible-ci/jenkins-master.yml"
    end
  end

end
