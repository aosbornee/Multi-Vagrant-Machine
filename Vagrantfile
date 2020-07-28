# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder ".", "/home/vagrant/app"
    app.vm.provision "shell", path: "environment/app/provision.sh", privileged: false

  end
  


  config.vm.define "db" do |subconfig|
    subconfig.vm.box = "ubuntu/xenial64"
    subconfig.vm.network "private_network", ip: "192.168.10.150"
    subconfig.hostsupdater.aliases = ["development.local"]
    subconfig.vm.synced_folder ".", "/home/vagrant/app"
    subconfig.vm.provision "shell", path: "environment/app/provision.sh", privileged: false
  end

end
end

