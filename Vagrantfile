Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", type:"virtualbox"
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true
  config.vm.provider "virtualbox" do |vm|
    vm.customize ["modifyvm", :id, "--memory", "2048"]
  end
   config.vm.provision "shell" do |s|
      s.inline = "yum -y update"
      s.privileged = true
  end
  config.vm.provision "shell" do |s|
      s.inline = "yum -y upgrade"
      s.privileged = true
  end
  config.vm.provision "shell" do |s|
    s.inline = "yum -y install git"
    s.privileged = true
  end
  config.vm.provision "ansible_local" do |ansible|
    ansible.galaxy_roles_path = '/vagrant/roles'
    ansible.galaxy_role_file = "/vagrant/requirements.yml"
    ansible.playbook = "/vagrant/site.yml"
    ansible.install_mode = "pip"
  end
end
