
# Docker Swarm
Running individual containers on multiple machines can be cumbersome. Docker Swarm eliminates the need to manually deploy containers on each node. A single-machine failure can bring down your entire application if your containers are running solely on that machine. Docker Swarm ensures high availability by automatically rescheduling containers to healthy nodes if a node fails. Docker Swarm simplifies container orchestration at scale, ensuring high availability, efficient resource utilization, and streamlined management of your containerized applications.

# Table of Contents
- Vangrantfile creation
- Define a unique IP for each machine
- Pre-install docker on each machine
  
# Vagrant File
A Vagrantfile is a configuration file used with Vagrant, a tool for managing virtual machines. It essentially acts as a blueprint for setting up your development environment.

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby  :

# Creates an object of 3 virtual machines with memory 1024, unique IP and assigns a docker image

machines = {
  "master" => {"memory" => "1024", "cpu" => "1", "ip" => "100", "image" => "bento/ubuntu-22.04"},
  "node01" => {"memory" => "1024", "cpu" => "1", "ip" => "101", "image" => "bento/ubuntu-22.04"},
  "node02" => {"memory" => "1024", "cpu" => "1", "ip" => "102", "image" => "bento/ubuntu-22.04"}
}
# Sets the Vagrant configuration version to "2" 
Vagrant.configure("2") do |config|

  machines.each do |name, conf|
# This line defines a virtual machine within the Vagrant configuration
    config.vm.define "#{name}" do |machine|
# Sets the box (pre-built VM image) for the virtual machine.
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
# Configures the network settings for the virtual machine. 
      machine.vm.network "private_network", ip: "10.10.10.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
# Memory allocation
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        
      end
      machine.vm.provision "shell", path: "docker.sh"
      
      if "#{name}" == "master"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end

    end
  end
end

```

