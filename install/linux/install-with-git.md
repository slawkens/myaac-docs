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

### **5. (optional) Change branch to develop to use latest features**

```bash
git checkout develop
```

You are done. If you did Step 5., then also follow next (optional) steps.

### **6. (optional) Install composer: https://getcomposer.org/**

### **7. (optional) Install dependencies**

After installing composer, install dependencies with following command

```bash
php composer.phar install
```

or just

```bash
composer install
```

(depends on how you installed the composer on your system)
