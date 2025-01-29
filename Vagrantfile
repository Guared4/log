Vagrant.configure("2") do |config|
  
  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 2
  end

  
  config.vm.define "logserver" do |log|
    log.vm.box = "bento/ubuntu-22.04"
    log.vm.hostname = "logserver"
    log.vm.network :private_network, ip: "192.168.57.10"
    
    log.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/log.yml"
      ansible.inventory_path = "inventory"
      ansible.extra_vars = {
        ansible_user: "vagrant",
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end
  end

  
  config.vm.define "webserver" do |web|
    web.vm.box = "bento/ubuntu-22.04"
    web.vm.hostname = "webserver"
    web.vm.network :private_network, ip: "192.168.57.20"
    web.vm.network "forwarded_port", guest: 80, host: 8080
    
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/log.yml"
      ansible.inventory_path = "inventory"
      ansible.extra_vars = {
        ansible_user: "vagrant",
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end
  end
end