# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
 
  config.vm.define  "haproxy"  do |haproxy|   #L1 naming
    haproxy.vm.box = "ubuntu/focal64"
    haproxy.vm.provider "virtualbox" do |vb1|
      vb1.name = "haproxy"          #L2 naming
    end
  
     haproxy.vm.hostname = "haproxy" #L3 naming
     haproxy.vm.network "private_network", type: "dhcp" , name: "VirtualBox Host-Only Ethernet Adapter"
     haproxy.vm.provision "shell", inline: <<-SHELL
      apt install --no-install-recommends software-properties-common -y
      add-apt-repository ppa:vbernat/haproxy-2.6 -y
      apt update
      apt install haproxy=2.6.\* -y
      systemctl enable haproxy
      rm /etc/haproxy/haproxy.cfg && cp /vagrant/haproxy.cfg /etc/haproxy/haproxy.cfg
      systemctl reload haproxy
      ifconfig | grep 192.168.105
     SHELL

  end
#================
  config.vm.define  "nginx"  do |nginx|   #L1 naming
    nginx.vm.box = "ubuntu/focal64"
    nginx.vm.provider "virtualbox" do |vb2|
      vb2.name = "nginx"          #L2 naming
    end
  
     nginx.vm.hostname = "nginx" #L3 naming
     nginx.vm.network "private_network", type: "dhcp" , name: "VirtualBox Host-Only Ethernet Adapter"
     nginx.vm.provision "shell", inline: <<-SHELL
      apt update
      apt install nginx -y
      systemctl enable nginx
      rm /etc/nginx/nginx.conf && cp /vagrant/nginx.conf /etc/nginx/nginx.conf
      systemctl reload nginx
      ifconfig | grep 192.168.105
     SHELL
  end
#=================
end
