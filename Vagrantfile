# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Kubernetes Master Server
  config.vm.define "kubemaster" do |kmaster|
    kmaster.vm.box = "centos/7"
    kmaster.vm.hostname = "kmaster.example.com"
    kmaster.vm.network "private_network", ip: "172.16.16.100"
    kmaster.vm.provider "virtualbox" do |v|
      v.name = "kubemaster"
      v.memory = 4048
      v.cpus = 2
    end
    #kmaster.vm.provision "shell", path: "bootstrap.sh"
  end

  NodeCount = 2

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "kworker#{i}" do |workernode|
      workernode.vm.box = "centos/7"
      workernode.vm.hostname = "kworker#{i}.example.com"
      workernode.vm.network "private_network", ip: "172.16.16.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "kworker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      #workernode.vm.provision "shell", path: "bootstrap.sh"
    end
  end

end
