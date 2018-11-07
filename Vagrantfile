# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.
	
  config.vm.hostname = "fedora4"

  config.vm.box = "ubuntu/xenial64"

  config.vm.network :forwarded_port, guest: 8080, host: 8080 # Tomcat
  config.vm.network :forwarded_port, guest: 9080, host: 9080 # Fixity and Reindexing

  config.vm.provider "virtualbox" do |v|
  	v.memory = 2048
  end

  shared_dir = "/vagrant"
	
  # Run Ansible from the Vagrant VM
  config.vm.provision "shell",
    inline: "apt-get update"
  config.vm.provision "shell",
    inline: "apt-get install software-properties-common"
  config.vm.provision "shell",
    inline: "apt-add-repository --yes --update ppa:ansible/ansible"
  config.vm.provision "shell",
    inline: "apt-get install -y ansible"
  # config.vm.provision "shell",
  #  inline: "cd /vagrant && ansible-galaxy install -f -p roles/ -r requirements.yml"

  config.vm.provision "ansible_local" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.galaxy_role_file = "requirements.yml"
    ansible.galaxy_roles_path = "./roles"
    ansible.playbook = "/vagrant/playbook.yml"
  end
  
end
