# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :

vmname = File.basename(File.expand_path(File.dirname(__FILE__)))

Vagrant.configure("2") do |config|

  # add our vagrant private ssh key if it exists
  vagrant_key = File.expand_path('~') + '/.ssh/vagrant'
  vagrant_key_pub = File.expand_path('~') + '/.ssh/vagrant.pub'
  if FileTest.exists?(vagrant_key) and FileTest.exists?(vagrant_key_pub)
    config.ssh.private_key_path = [ vagrant_key, "~/.vagrant.d/insecure_private_key" ]
  end

  config.vm.define vmname do |ap|
    ap.vm.box = "opscode-debian-7.2.0"
    ap.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_debian-7.2.0_chef-provisionerless.box"
    ap.vm.hostname = vmname

    ap.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--cpuexecutioncap", "100"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
      v.customize ["modifyvm", :id, "--memory", 512]
    end

    ap.vm.network :private_network, ip: "10.0.0.40"

    if config.ssh.private_key_path.kind_of?(Array) and config.ssh.private_key_path.include? vagrant_key
      ap.vm.provision :shell do |shell|
        vagrant_key_pub_content = File.read(vagrant_key_pub)
        shell.inline = "echo '#{vagrant_key_pub_content}' > /home/vagrant/.ssh/authorized_keys && chmod 600 /home/vagrant/.ssh/authorized_keys"
      end
    end

    ap.vm.provision :ansible do |ansible|
      ansible.playbook = "docker-debian.yml"
      ansible.verbose = 'vvvv'
    end
  end
end
