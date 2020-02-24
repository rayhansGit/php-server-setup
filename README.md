# php-server-setup
sudo apt-get update -y
sudo apt-get install apache2 -y
sudo systemctl start apache2.service

# Install mysql
sudo apt-get install mysql-server -y

# Install PHP version 7.2 
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.2
sudo apt-get install -y php7.2-{pdo,memcache,memcached,mysql,gd,gmp} && sudo apt-get install libapache2-mod-php  -y

# Install additional setup
sudo apt-get install curl php7.2-cli php7.2-mbstring git unzip memcached
cd ~

# Install composer
sudo apt install composer -y

# Setup REST-API (flight-PHP) project
sudo rm -r /var/www/html/*
sudo git clone https://github.com/sabbir-rupom/rest-api-flight-PHP.git /var/www/html/
cd /var/www/html/
sudo composer update

#
# Allow mod_rewrite for .htaccess
# Change to document root [ /var/www AllowOverwrite All ]
#
sudo vi /etc/apache2/apache2.conf  
sudo a2enmod rewrite
sudo systemctl restart apache2

# Configure web server 
sudo mv /var/www/html/app/config/example.config_app.ini /var/www/html/app/config/config_app.ini
sudo chown -R ubuntu:ubuntu /var/www/html/app/config/config_app.ini
sudo chmod -R 755 /var/www/html/app/config/config_app.ini
sudo chown -R www-data:www-data /var/www/html/uploads/
sudo chmod -R 775 /var/www/html/uploads/
sudo chown -R www-data:www-data /var/www/html/cache/
sudo chmod -R 755 /var/www/html/cache/
sudo chown -R www-data:www-data /var/www/html/log/
sudo chmod -R 755 /var/www/html/log/
