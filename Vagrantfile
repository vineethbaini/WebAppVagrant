
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.define :db1 do |db|
    db.vm.host_name="db1"
    db.vm.network "private_network", ip: "192.168.99.90"
    db.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", "1024"]
          vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
  end
  (1..2).each do |i|
    config.vm.define :"app#{i}" do |app_c|
      app_c.vm.host_name="app#{i}"
      app_c.vm.network "private_network", ip: "192.168.99.#{i}"
      app_c.vm.network "forwarded_port", guest: 80, host: "809#{i}"
      app_c.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
        end
      end
    end
    config.vm.provision :ansible do |ansible|
       ansible.playbook = "playbook.yml"

   end
end
