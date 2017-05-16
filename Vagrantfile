
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = false
  config.vm.define :db1 do |db|
    db.vm.host_name="db1"
    db.vm.network "private_network", ip: "192.168.99.90"
  end
  (1..2).each do |i|
    config.vm.define :"app#{i}" do |app_c|
      app_c.vm.host_name="app#{i}"
      app_c.vm.network "private_network", ip: "192.168.99.7#{i}"
      app_c.vm.network "forwarded_port", guest: 80, host: "809#{i}"
      end
    end
    config.vm.provision :ansible do |ansible|
       ansible.playbook = "playbook.yml"

   end
end
