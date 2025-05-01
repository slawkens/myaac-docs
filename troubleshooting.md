---
description: Solutions to common problems
---

# Troubleshooting

Remember there is also FAQ section on my-aac.org website: [https://my-aac.org/faqs/](https://my-aac.org/faqs/)

## 1. Errors on installation page

### 1. ZIP Extension not found

MyAAC needs PHP ZIP extension to install plugins.

The extension can be easily enabled in php.ini.

#### Linux

On linux it's even easier because you just need to install following package:

```
sudo apt install php-zip
```

Then restart your webserver:

```
sudo service nginx restart
```

```
sudo service apache restart
```

#### Windows (XAMPP)

Go to Apache -> Config -> php.ini

Uncomment&#x20;

;extension=zip

By removing semicolon ; from it

#### [Windows (Uniform Server)](install/windows/uniform-server-recommended.md)

### 2. config.lua not found

#### There is problem with finding config.lua on linux

It's a problem with permissions file\_exists(config.lua) returns false, even though the file exists

The current solution is to set execute flags on every folder above ots path. So if your config.lua (server) is located in: /home/myuser/forgottenserver/config.lua, then you need to execute following commands:

```
chmod +x /home
chmod +x /home/myuser
chmod +x /home/myuser/forgottenserver
```

And then refresh the installation page again and follow the instructions

## 2. Plugins

### 1. gesior-shop-system - PayPal Points are not being delivered / not coming

1. Ensure you have SSL (https) enabled. This is required for PayPal to safely deliver Instant Payment Notifications (IPNs). You can generate a free SSL certificate via Certbot tool. Just visit its website - [https://certbot.eff.org/](https://certbot.eff.org/) and follow the instructions for your OS / web server.
2. If you are using Cloudflare, you need to add an rule to ignore PayPal IPs. (to do: add screenshots/instructions how to do it).
3. Additionally you can check PayPal IPN History to see the status of requests being sent to your web server. The IPN Status page if available under this address - [https://www.paypal.com/merchantnotification/ipn/history](https://www.paypal.com/merchantnotification/ipn/history)
4. If you become following entry in system/logs/paypal_error.log

`[Thu, 01 May 2025 23:13:50 +0200] Payment status is 'Pending'. Points will be added automatically after status is changed to 'completed'. Please wait.`

It means the account email on PayPal website is not verified.

