required = ["vagrant-docker-compose", "vagrant-cachier"]

restart = false
for req in required
    unless Vagrant.has_plugin?(req)
      system "vagrant plugin install #{req}"
      puts "Dependencies #{req} installed."
      restart = true
    end
end

if restart then
    puts "Dependencies installed, please relaunch vagrant up."
    exit
end


Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/xenial64"

  config.vm.network "forwarded_port", guest: 3000, host: 3000

  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", run: "always"

  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.memory = 4096
  end
end
