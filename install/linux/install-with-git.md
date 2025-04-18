# Install with git

Next we will download & install MyAAC with git.

### 1. Install git

```bash
sudo apt install git
```

### 2. Enter the desired folder where you want to install myaac.

On linux, this can be /var/www

```bash
mkdir /var/www && cd /var/www
```

### 3. Clone the repository from github

```bash
git clone https://github.com/otsoft/myaac.git
```

### 4. Enter the folder

```bash
cd myaac
```

### 5. Adjust file permissions

Change file owner to www-data (web user)
```bash
sudo chown -R www-data:www-data /var/www/*
```

Set proper file flags (with chmod)
```bash
sudo chmod 660 images/guilds
sudo chmod 660 images/houses
sudo chmod 660 images/gallery
sudo chmod -R 760 system/cache
```

### 6. Install Composer
Visit [https://getcomposer.org/](https://getcomposer.org/) for more instructions.

### 7. Install Composer dependencies

After installing composer, install dependencies with following command

```bash
php composer.phar install
```

or just

```bash
composer install
```

(depends on how you installed the composer on your system)

### 8. Install NPM
Visit [https://docs.npmjs.com/downloading-and-installing-node-js-and-npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) for more instructions.

### 9. Install NPM dependencies
```bash
npm install
```