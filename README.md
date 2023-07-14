Setup

install nginx - php-fpm and butterfly
```
        sudo apt-get install nginx php-fpm
```
edit /etc/nginx/sites-available/default, change version and domainname
```
        server {
            listen 80 default_server;
            listen [::]:80 default_server;

            root /var/www/html;
            index index.php index.html index.htm;

            server_name yourdomain.com;

            location / {
                try_files $uri $uri/ /index.php?$query_string;
            }

            location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php<version>-fpm.sock;
            }

            location ~ /\.ht {
                deny all;
            }
        }
```
Test your nginx configuration
``` 
        sudo nginx -t

```

After you have tested your configuration, you will need to restart both nginx and PHP-FPM for the changes to take effect. You can do this with the following commands:

```
        sudo systemctl restart nginx
        sudo systemctl restart php<version>-fpm
```

Note: Dont forget to edit the ```<version>``` tag in your configuration.

---------
Developed by the-abra
