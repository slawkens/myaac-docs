# Install with git

### 1. **Install git**

```bash
sudo apt install git
```

### **2. Enter the desired folder where you want to install myaac.**

On linux, this can be /var/www

```bash
cd /var/www
```

### **3. Clone the repository from github**

```bash
git clone https://github.com/otsoft/myaac.git
```

### **4. Enter the folder**

```bash
cd myaac
```

### **5. (optional) Change branch to develop to use latest features (use just to test things, do not use on production server - you have been warned!)**

```bash
git checkout develop
```

### **6. Install Composer**
Visit [https://getcomposer.org/](https://getcomposer.org/) for more instructions.

### **7. Install Composer dependencies**

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

### 9. Install NPN dependencies
```bash
npm install
```