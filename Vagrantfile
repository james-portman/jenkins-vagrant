Vagrant.configure("2") do |config|
  config.vm.define "jenkins"
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "virtualbox" do |v|
    v.name = "jenkins"
  end
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  # Python 2.7 is missing from the base image, so:
  config.vm.provision "shell" do |shell|
    shell.inline = "sudo --preserve-env apt update; sudo --preserve-env apt install -y python"
    shell.env = {"http_proxy": "#{ENV['http_proxy']}"}
  end
  # Run Ansible role:
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.galaxy_roles_path = ".vagrant/roles"
    ansible.galaxy_role_file = "requirements.yml"
  end
end
