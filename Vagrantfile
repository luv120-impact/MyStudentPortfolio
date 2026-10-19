Vagrant.configure("2") do |config|

  # CentOS Stream 9
  config.vm.box = "eurolinux-vagrant/centos-stream-9"

  # YMB hostname
  config.vm.hostname = "ymb-zone-b-dev"

  # YMB private network
  config.vm.network "private_network", ip: "192.168.56.13"

  # VirtualBox resources
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end

  # Automatic provisioning
  config.vm.provision "shell", inline: <<-SHELL

    # Install required packages
    yum install httpd wget unzip zip vim -y

    # Start and enable httpd
    systemctl start httpd
    systemctl enable httpd

    # Deploy Lovedeep Singh's portfolio
    cp /vagrant/index.html /var/www/html/index.html

    rm -rf /var/www/html/css
    rm -rf /var/www/html/assets

    cp -r /vagrant/css /var/www/html/css
    cp -r /vagrant/assets /var/www/html/assets

    # Activity 2.2 provisioning date
    date > /var/www/html/status.txt

    # Restart httpd
    systemctl restart httpd

  SHELL

end