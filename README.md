# aws-server-creation
Commands for aws server creation

```
Step1: chmod 400 aws-instance-key.pem
Step2: ssh -i aws-instance-key.pem mailto:ubuntu@ec2-74-327-94-56.compute-1.amazonaws.com

Step3: sudo apt update && sudo apt upgrade -y
Step4: sudo apt install nginx -y
Step5: sudo systemctl enable nginx
Step6: sudo systemctl start nginx

Step7: sudo apt install php8.2
Step8: sudo apt install php8.2-mysql php8.2-xml php8.2-mbstring php8.2-zip php8.2-curl php8.2-bcmath php8.2-fpm php8.2-cli php8.2-common php8.2-gd
Step 9: sudo systemctl enable php8.2-fpm
Step 10: sudo systemctl start php8.2-fpm
Step 11: sudo systemctl status php8.2-fpm

Step 12: sudo systemctl restart nginx 
Step 13: sudo nginx -t

Step 14: sudo apt install mysql-server -y
Step 15: sudo mysql_secure_installation
Step 16: sudo apt install phpmyadmin -y
Step 17: sudo mysql -u root -p

Step 18: 
CREATE DATABASE your_project_database;
CREATE USER 'root'@'localhost' IDENTIFIED BY 'root';
GRANT ALL PRIVILEGES ON your_project_database.* TO 'root'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Step 19: sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

Step 20: sudo systemctl restart nginx

Step 21: 
curl -sS https://getcomposer.org/installer -o composer-setup.php
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

Step 22:
ssh-keygen -t ed25519 -C "your_email@example.com"
-or-
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
cat ~/.ssh/id_ed25519.pub
**added the key in GIT Repository

Step 23:
sudo systemctl restart php8.2-fpm
sudo systemctl restart nginx

Step 24:
sudo service nginx status
sudo systemctl status php8.2-fpm

Site Config
=====================================================
server {
    listen 80;
    server_name 96.225.95.32;  # Replace with your domain or IP address
    root /var/www/html/aws-instance/public;

    index index.php index.html index.htm;

    location / {
        add_header 'Access-Control-Allow-Origin' '*';
        try_files $uri $uri/ /index.php?$query_string;
    }

     location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;  # Adjust for your PHP version
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    error_log /var/log/nginx/laravel_error.log;
    access_log /var/log/nginx/laravel_access.log;

    location /phpmyadmin {
    root /usr/share/;  # Path where phpMyAdmin is installed
    index index.php index.html index.htm;
    location ~ ^/phpmyadmin/(.*\.php)$ {
       fastcgi_pass unix:/run/php/php8.2-fpm.sock;  # Ensure this matches your PHP version
       fastcgi_index index.php;
       include fastcgi_params;
       fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
    location ~* \.(jpg|jpeg|gif|css|png|js|ico|html)$ {
       expires max;
       log_not_found off;
    }
   }
}

```
