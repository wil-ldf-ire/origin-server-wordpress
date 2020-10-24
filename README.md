# wordpress on origin server

```
installpath="/var/www/html"
read -p "Website Domain: " websitedomain
read -p "IP Address: " ipv4address
sudo chown ubuntu:ubuntu $installpath/$websitedomain -R
sudo git clone https://github.com/wil-ldf-ire/origin-wordpress.git $installpath/$websitedomain/origin-wordpress
sudo cp $installpath/$websitedomain/origin-wordpress/nginx.conf /etc/nginx/sites-available/$websitedomain
sudo sed -i 's/your_server_ip/$ipv4address/g' /etc/nginx/sites-available/$websitedomain
sudo sed -i 's/your_server_domain/$websitedomain/g' /etc/nginx/sites-available/$websitedomain
sudo ln -s /etc/nginx/sites-available/$websitedomain /etc/nginx/sites-enabled/$websitedomain
sudo cp $installpath/$websitedomain/origin-wordpress/apache2.conf /etc/apache2/sites-available/$websitedomain.conf
sudo sed -i 's/your_server_domain/$websitedomain/g' /etc/apache2/sites-available/$websitedomain.conf
sudo sed -i "s/your_server_path/$installpath1/g" /etc/apache2/sites-available/$websitedomain.conf
a2ensite $websitedomain
sudo systemctl reload nginx
sudo service apache2 start
sudo certbot --agree-tos --no-eff-email --email tech@wildfire.world --nginx -d $websitedomain -d www.$websitedomain
sudo service apache2 restart;

```