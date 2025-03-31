# Configure web server

Next step is to configure web server, so it will serve our website.

There are many possible options to use, but in this tutorial we will just cover the two most populars: 1) apache2 and 2) nginx.

## Option 1: apache2

### **1. Install apache2 with php and all required extensions if you still didn't have.**

```bash
sudo apt install -y apache2 php php-zip php-xml php-mysql 
```

### **2. Edit `/etc/apache2/sites-enabled/default`**

Set `DocumentRoot` to path, where you previously downloaded MyAAC.

We did it in `/var/www/myaac`, so lets point our server to it.

```
DocumentRoot /var/www/myaac
```

### **3. Add following directives between `<VirtualHost>` block.**

```
<Directory "/var/www/myaac">
        AllowOverride all
        Order Deny,Allow
        Allow from all
        Require all granted
</Directory>
```

With this we say that we allow all users to access our website, and that we allow customisations through .htaccess files.

### **4. Restart apache**

```bash
sudo service apache2 restart
```

## Option 2: nginx

### **1. Install nginx with php and all required extensions if you still didn't have.**

```
sudo apt install -y nginx php-fpm php-zip php-xml php-mysql 
```

### **2. Edit `/etc/nginx/sites-enabled/default`**

You can take following configuration as an example:

```
server {
	listen 80;
	root /home/otserv/www/public;
	index index.php;
	server_name your-domain.com;

	# increase max file upload
	client_max_body_size 10M;

	# this is very important, be sure its in your nginx conf - it prevents access to logs etc.
	location ~ /system {
		deny all;
	}

	# block .htaccess, CHANGELOG.md, composer.json etc.
	# this is to prevent finding software versions
	location ~\.(ht|md|json|dist)$ {
		deny all;
	}

	# block git files and folders
	location ~ /\.git {
		deny all;
	}

	location / {
		try_files $uri $uri/ /index.php?$query_string;
	}

	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_read_timeout 240;
		fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
		# for ubuntu 22.04+ it will be php8.1-fpm.sock
	}
}
```

Replace server\_name with your domain, and adjust fastcgi\_pass to your PHP version.

### **3. Restart nginx**

```bash
sudo service nginx restart
```
