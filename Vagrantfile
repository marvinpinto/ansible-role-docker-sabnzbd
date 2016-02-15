$script = <<SCRIPT
sudo apt-get install -qq -y python-pip python-dev
sudo pip install ansible
echo -ne "[defaults]\nroles_path=/opt/ansible_roles\n" > /home/vagrant/.ansible.cfg
sudo mkdir -p /opt/ansible_roles
sudo chown -R vagrant: /opt/ansible_roles
ansible-galaxy install -p /opt/ansible_roles marvinpinto.docker
ln -fTs /vagrant /opt/ansible_roles/ansible-role-docker-sabnzbd
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end

  config.vm.provision "shell", inline: $script

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "tests/test.yml"
    ansible.install = false
  end
end
