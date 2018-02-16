# -*- mode: ruby -*-
# vi: set ft=ruby :

#
# Refer to README for usage. Only one VM can be spun up at once because of port forwarding conflicts.
# If VM_GUI=true or TESTING=true then port forwarding is not run.
#

PROJECT_NAME = ENV['PROJECT_NAME'] || File.basename(File.expand_path(File.dirname(__FILE__)))

#
# Environment variables that can be overriden on vagrant up
#
VM_CPUS = ENV['VM_CPUS'] || 1
VM_CPU_CAP = ENV['VM_CPU_CAP'] || 100
VM_MEMORY = ENV['VM_MEMORY'] || 6144
VM_VB_NATDNSHOSTRESOLVER = ENV['VM_VB_NATDNSHOSTRESOLVER'] || 'off'

boxes = [
  {
  :name => "exsi",
  :box => "david-flynn/esxi-6.5.0-base",
  :cpu => VM_CPU_CAP,
  :ram => VM_MEMORY
  }
]

Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = VB_GUEST
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
    if(HTTP_PROXY.nil? || HTTP_PROXY.empty? || HTTP_PROXY == 'null')
      puts "Disabling proxy conf plugin. No proxy settings found."
      config.proxy.enabled = false
    else
      config.proxy.http = HTTP_PROXY
      config.proxy.https = HTTPS_PROXY
      config.proxy.no_proxy = NO_PROXY
    end
  end

  boxes.each do |box|
    config.vm.define box[:name], primary: box[:primary] do |vms|
      vms.vm.box = box[:box]

      vms.vm.synced_folder '.', '/vagrant', type: 'virtualbox' , disabled: false

      vms.vm.provider "virtualbox" do |v|
        v.gui = true
        v.cpus = VM_CPUS
        v.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        v.customize ["modifyvm", :id, "--memory", box[:ram]]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
        v.customize ["modifyvm", :id, "--natdnshostresolver1", VM_VB_NATDNSHOSTRESOLVER]
        v.customize ['modifyvm', :id, '--cableconnected1', 'on']
      end
    end
  end

end
