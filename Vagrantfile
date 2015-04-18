$setup = <<SETUP
sudo -i
apt-get update
debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
apt-get install -y apache2 mysql-server libapache2-mod-auth-mysql php5-mysql php5 libapache2-mod-php5
rm -rf /var/www/html
ln -fs /vagrant/public /var/www/html
a2enmod rewrite
cat >/etc/apache2/sites-available/000-default.conf <<EOL
<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html
	ErrorLog /var/log/apache2/error.log
	CustomLog /var/log/apache2/access.log combined
	<Directory /var/www/html >
		AllowOverride All
	</Directory>
</VirtualHost>
EOL
sed -i "s/error_reporting = .*/error_reporting = E_ALL/" /etc/php5/apache2/php.ini
sed -i "s/display_errors = .*/display_errors = On/" /etc/php5/apache2/php.ini
service apache2 restart
SETUP

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "shell", inline: $setup
  config.vm.network :forwarded_port, host: 8080, guest: 80
  config.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=666"]
  config.vm.hostname = "vagrant"
end
