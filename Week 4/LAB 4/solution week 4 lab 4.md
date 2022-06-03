coonect to my instance 
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo systemctl start mariadb
mysql -u root -p
CREATE USER 'raphael-wordpress'@'localhost' IDENTIFIED BY 'Raphael@1234';
CREATE DATABASE `wordpress-db`;
GRANT ALL PRIVILEGES ON `wordpress-db`.* TO "raphael-wordpress"@"localhost";
FLUSH PRIVILEGES;
exit
cp wordpress/wp-config-sample.php wordpress/wp-config.php
nano wordpress/wp-config.php