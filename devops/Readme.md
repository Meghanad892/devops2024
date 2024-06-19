Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"
  config.vm.network "public_network"
  config.hostmanager.enabled = true

  
  config.vm.define "web01" do |web01|
    web01.vm.box = "ubuntu/xenial64"
	web01.vm.hostname = 'web01.example.com'
	web01.vm.network "private_network", ip: "192.168.11.12"
	web01.disksize.size = '50GB'
  end
  
  config.vm.define "db01" do |db01|
    db01.vm.box = "centos/7"
	db01.vm.hostname = 'db01.example.com'
	db01.vm.network "private_network", ip: "192.168.11.13"
	db01.vm.provider "virtualbox" do |vb|
     vb.memory = "1600"
	 vb.cpus = 2
   end
  end
 end
