# Ansible command is at the very bottom of this Vagrantfile

Vagrant.configure("2") do |config|
  config.vm.define "VM1", primary: true do |vm1|
    vm1.vm.box = "centos/7"

=begin
       Config files below are provisioned with shell to avoid permissions
       issues with file provisioner that works under vagrant user by default
=end

    vm1.vm.provision "shell", inline: <<-SHELL
yum -y install epel-release
yum -y install ansible
bash --verbose -c 'cat /vagrant/key.pub >> /home/vagrant/.ssh/authorized_keys'
mkdir --verbose /etc/ansible/
bash --verbose -c 'echo -e "\
---\n\
all:\n\
  children:\n\
    VM1:\n\
      hosts:\n\
        vm1:\n\
          ansible_user: vagrant\n\
          ansible_host: 192.168.10.10\n\
          ansible_ssh_private_key_file: /vagrant/key\n\
    VM2:\n\
      hosts:\n\
        vm2:\n\
          ansible_user: vagrant\n\
          ansible_host: 192.168.10.11\n\
          ansible_ssh_private_key_file: /vagrant/key\n\
    VM3:\n\
      hosts:\n\
        vm3:\n\
          ansible_user: vagrant\n\
          ansible_host: 192.168.10.12\n\
          ansible_ssh_private_key_file: /vagrant/key\n\
...\
" >> /etc/ansible/hosts'
bash --verbose -c 'echo -e "\
[defaults]\n\
host_key_checking = false\
" >> /home/vagrant/.ansible.cfg'
    SHELL

    vm1.vm.network "private_network", ip: "192.168.10.10"
  end



  config.vm.define "VM2" do |vm2|
    vm2.vm.box = "ubuntu/xenial64"

    vm2.vm.provision "shell", inline: <<-SHELL
bash --verbose -c 'cat /vagrant/key.pub >> /home/vagrant/.ssh/authorized_keys'
    SHELL

    vm2.vm.network "private_network", ip: "192.168.10.11"
  end



  config.vm.define "VM3" do |vm3|
    vm3.vm.box = "ubuntu/xenial64"

    vm3.vm.provision "shell", inline: <<-SHELL
bash --verbose -c 'cat /vagrant/key.pub >> /home/vagrant/.ssh/authorized_keys'
    SHELL

    vm3.vm.network "private_network", ip: "192.168.10.12"
  end
end

__END__

ansible-playbook /vagrant/playbook.yml
