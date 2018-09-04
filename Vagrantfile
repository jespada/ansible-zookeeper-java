# Before starting any boxes
#  'vagrant plugin install vagrant-hostmanager'
#  'vagrant plugin install vagrant-vbguest'


nodes = [
  { :hostname => 'zookeeper01', :ip => '192.168.33.10', :ram => 512 },
  { :hostname => 'zookeeper02', :ip => '192.168.33.11', :ram => 512 },
  { :hostname => 'zookeeper03', :ip => '192.168.33.12', :ram => 512 }
]


Vagrant.configure("2") do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  nodes.each do |node|
    config.vm.define node[:hostname] do |cfg|
      cfg.vm.box = "ubuntu/xenial64"
      cfg.vm.hostname = node[:hostname]
      cfg.vm.network :private_network, ip: node[:ip]

      memory = node[:ram]
      cfg.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--memory", memory.to_s,
          "--cpus", "1"
        ]
      end

      cfg.vm.provision "shell",
                       inline: "sed -i '/127.0.1.1\t#{node[:hostname]}\t#{node[:hostname]}/d' /etc/hosts"

      cfg.vm.provision "ansible_local" do |ansible|
        ansible.install = true
        ansible.playbook = "playbook.yml"
        ansible.compatibility_mode = "2.0"

        # ansible.groups = {
        #   "zookeepers" => ['zookeeper01', 'zookeeper02', 'zookeeper03']
        # }
      end

    end
  end
end
