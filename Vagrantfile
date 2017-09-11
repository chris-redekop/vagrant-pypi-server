$script = <<SCRIPT
apt-get -y update
apt-get -y upgrade python3
apt-get -y install python3-pip

pip3 install --upgrade pip passlib pypiserver

mkdir /packages
chmod 755 /packages

#chmod 755 /home/ubuntu/pypi-service.sh

mv /tmp/pypi-server.service /etc/systemd/system
chmod 644 /etc/systemd/system/pypi-server.service

systemctl start pypi-server
systemctl enable pypi-server
SCRIPT

Vagrant.configure('2') do |config|
  config.vm.provider "virtualbox" do |vb, override|
    override.vm.box = "ubuntu/xenial64"
  end

  config.vm.provision "file", source: "files/pypi-server.service", destination: "/tmp/pypi-server.service"
  config.vm.provision "shell", inline: $script

  config.vm.network :forwarded_port, guest: 8080, host: 8080
end
