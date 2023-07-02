Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.define "ansible-alura" do |m|
      m.vm.network "private_network", ip: "192.168.56.10"
  end

end
