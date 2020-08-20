# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider :libvirt do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.define "syslog" do |syslog|
    syslog.vm.box = "centos/7"
    syslog.vm.hostname = "syslog"
  end

  config.vm.define "logstash" do |logstash|
    logstash.vm.box = "centos/7"
    logstash.vm.hostname = "logstash"
    logstash.vm.provision :ansible do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.compatibility_mode = "2.0"
      ansible.limit = "all"
    end
  end

end
