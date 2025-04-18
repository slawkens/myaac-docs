# Install with git

Next we will download & install MyAAC with git.

### 1. Install git

```bash
sudo apt install git
```

### 2. Enter the desired folder where you want to install myaac.

On linux, this can be /var/www

```bash
cd /var/www
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

TLDR: (Execute following commands to install the latest version of Node.js and NPM on Ubuntu)

#### 1. Download NVM (Node Version Manager)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```
#### 2. Reconnect ssh client (for example: Exit and login with putty)
#### 3. Verify installation

```bash
command -v nvm
```

If it's ok, you should see "nvm" printed.

#### 4. Install node
```bash
nvm install node # "node" is an alias for the latest version
```

#### 5. Update NPM to latest version
```bash
npm install -g npm
```

### 9. Install NPM dependencies

If you followed the 8. Step, you should have NPM installed. Now you can install the dependencies.

```bash
cd /var/www/myaac
npm install
```