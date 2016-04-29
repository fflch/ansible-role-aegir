# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.hostname = 'aegir.local'
  config.vm.network 'private_network', ip: '10.55.55.55'

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
  end

  config.vm.provision "shell" do |s|
    s.inline = <<-SHELL
      cd /vagrant
      make deps-ansible
      make ansible
      . d
      make ansible-playbook-test
    SHELL
    s.env = {
      'ANSIBLE_REQUIREMENTS' => 'tests/roles/git_requirements.yml',
      'ANSIBLE_ROLES_PATH'   => 'tests/roles',
      'ANSIBLE_PLAYBOOK'     => 'tests/playbooks/git.yml',
      'PYTHONUNBUFFERED'     => '1',
      'ANSIBLE_FORCE_COLOR'  => 'true',
    }
    s.keep_color = true
  end

end
