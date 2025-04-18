# Configure web server

First we will configure the web server, so it will serve our website.

There are many possible options to use, but in this tutorial we will just cover the two most populars: 
1) [apache2](#option-1-apache2) and
2) [nginx](#option-2-nginx)

### Update system first

Before we continue, lets ensure we have the latest list of packages for our system:

```bash
sudo apt update
```

## Option 1: apache2

### **1. Install apache2 with php and all required extensions if you still didn't have.**

```bash
sudo apt install -y apache2 php php-zip php-xml php-mysql php-gd
```

### **2. Edit `/etc/apache2/sites-enabled/default.conf` or `000-default.conf`**

Set `DocumentRoot` `/var/www/myaac`.

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
sudo apt install -y nginx php-fpm php-zip php-xml php-mysql php-gd
```

### **2. Edit `/etc/nginx/sites-enabled/default`**

You can take following configuration as an example:
[nginx-sample.conf](https://raw.githubusercontent.com/slawkens/myaac/refs/heads/main/nginx-sample.conf)

Don't copy it 1:1, but take it as example, how your config might look like.

Replace server\_name with your domain, and adjust fastcgi\_pass to your PHP version.

The most important parts of this config, are those two:

#### 1.
```
location ~ /system {
    deny all;
}
```
This one blocks access to system folder, where logs and source code is stored: If you don't add it, anyone will be able to read your PayPal logs (for example)!!!

#### 2.
```
location / {
    try_files $uri $uri/ /index.php?$query_string;
}
```
This one is not so dangerous, but without it, you won't be able to see some pages:

### **3. Restart nginx**

Finally, we can restart the nginx to make our changes happen.

```bash
sudo service nginx restart
```
