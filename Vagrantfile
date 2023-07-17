Vagrant.configure("2") do |config|

  config.vm.box = "nitindas/ubuntu-22"

  config.vm.define "wordpress" do |m|
      m.vm.network "private_network", ip: "192.168.56.10"
  end

  config.vm.define "mysql" do |m|
    m.vm.network "private_network", ip: "192.168.56.11"
  end

end
