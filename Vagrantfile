Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 386
    v.cpus = 1
  end
  config.vm.box = "ubuntu/xenial64"
  config.vm.define "mgr" do |mgr|
    mgr.vm.hostname = "mgr.site"
    mgr.vm.network :private_network, ip: "192.168.50.19"
    mgr.vm.network :forwarded_port, guest: 80, host: 8000, auto_correct: true
    mgr.vm.provision  "shell", path: "bootstrap.sh"
  end
end
