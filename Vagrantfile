# -*- mode: ruby -*-
# vi: set ft=ruby :

# Ensure role dependencies are in place
if [ "up", "provision" ].include?(ARGV.first) && File.directory?("roles") &&
  !(File.directory?("roles/azavea.fpm") || File.symlink?("roles/azavea.fpm"))
  system("ansible-galaxy install --force -r roles.yml -p roles")
end

# Targeting RHEL6
Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-6.9"
  config.vm.host_name = "bento-centos69" # Determines 'Build Host' in resulting RPM
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.config_file = "ansible.cfg"
    ansible.compatibility_mode = "2.0"
    # ansible.verbose = true
  end
end
