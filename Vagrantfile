Vagrant.configure("2") do |config|
  config.vm.box_check_update = false

  config.vm.define :node1 do |node|
  node.vm.box = "puphpet/centos65-x64"
   node.vm.network "private_network", ip: "10.0.0.10"
end

  config.vm.define :node2 do |node|
  node.vm.box = "puphpet/centos65-x64"
   node.vm.network "private_network", ip: "10.0.0.20"
end

   config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.memory = "2048"
     vb.cpus = "2"
end

  config.vm.provision "shell" do |s|
   s.inline = <<-SHELL
      yum -y install libselinux-python
      SHELL
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"

    ansible.groups = {
      "master" => ["node1"],
      "slave"  => ["node2"]
   }
  end
end
