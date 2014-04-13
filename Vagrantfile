# -*- mode: ruby -*-
# vi: set ft=ruby :


$lamp = <<LAMP

apt-get update

apt-get install -y apache2
rm -rf /var/www
ln -fs /vagrant/www /var/www

apt-get install -y libapache2-mod-php5

# this one keeps failing because it requires a password to be set
# apt-get install -y mysql-server
apt-get install -y libapache2-mod-auth-mysql
apt-get install -y php5-mysql

a2enmod rewrite
a2enmod php5
sed -i '/AllowOverride None/c AllowOverride All' /etc/apache2/sites-available/default
service apache2 restart

LAMP

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.provision :shell, inline: $lamp
  config.vm.network :forwarded_port, host: 4000, guest: 80
end
