Vagrant.configure("2") do |config|
  config.vm.box = "eurolinux-vagrant/centos-stream-9"

  # Proxy Sunucusu (Nginx)
  config.vm.define "proxy01" do |proxy|
    proxy.vm.hostname = "proxy01"
    proxy.vm.network "private_network", ip: "192.168.50.10"
    proxy.vm.provider "virtualbox" do |vb|
      vb.name = "lab-proxy01"
      vb.memory = 512
      vb.cpus = 1
    end
  end

  # Web Sunucusu (Apache)
  config.vm.define "web01" do |web|
    web.vm.hostname = "web01"
    web.vm.network "private_network", ip: "192.168.50.11"
    web.vm.provider "virtualbox" do |vb|
      vb.name = "lab-web01"
      vb.memory = 512
      vb.cpus = 1
    end
  end

  # Database Sunucusu (MariaDB)
  config.vm.define "db01" do |db|
    db.vm.hostname = "db01"
    db.vm.network "private_network", ip: "192.168.50.12"
    db.vm.provider "virtualbox" do |vb|
      vb.name = "lab-db01"
      vb.memory = 512
      vb.cpus = 1
    end
  end
end
