# About plugins

MyAAC allows customisations with so called Plugins system.

Plugins are distributed using .zip archives.

## What can be done with plugins

* Themes (old: templates)
* Pages
* Other custom content

## Install

Visit Admin Page of your server - your-domain.net/admin and from menu go to **Plugins**.

## Remove / Uninstall

Plugins can be removed, which erases all the files. Database changes are not reverted. That means any change that plugin made to your database, like adding new table or columns, will **NOT** be removed on removal. This is subject to change, in future versions of MyAAC. Not all plugin can be uninstalled, some of them may require manual remove from file system.

## Develop

This section should give some basic overview about plugins architecture.

### Structure

* plugins/
  * your-plugin.json
  * your-plugin/ (directory)
    * all files that your plugins uses should be placed here.
    * (applies only to 0.8) Except files like templates and pages that currently needs to be placed outside of this folder
      * templates in templates/ folder
      * pages in system/pages/
    * (applies only to 1.0+) you can put custom content in the following folders under the plugin:
      * pages/
      * themes/
      * and commands/
    * This allows for high customization through the plugins

### Definition File

Every plugin needs to define some basic options in file called plugin-name.json

Description of attributes in this file:

* **name** Short name of your plugin
* **description** (optional) Briefly description
* **version** Current version of the plugin. In future it may be used to do automatic updates of the plugins.
* **author** (optional) Author or authors of the plugin
* **contact** (optional) Any preferred way to contact the developer. May be e-mail or website.
*   **require** (optional) You can define a requirements for your plugin, without them your plugin will be not allowed to install.

    This includes:

    * myaac version
    * php version
    * database version
    * columns in database
    * tables in database
    * PHP Extensions
    * other plugins

    The requirements with underslash (\_) are in Semantic Versioning format ([https://semver.org/](https://semver.org/)), that tools like Composer are using. These have more options, like defining maximum version.
* **install** (optional) The file specified here will be executed after files has been extracted, using PHP built-in _require_ function. You can install database tables here, or do any other operations that should be done only once.
* **uninstall** (optional) This is **not** opposide to "install". Instead, the files defined here will be deleted after user decides to uninstall the plugin.
* **hooks** (optional) Hooks allows executing your code in the specific place of the MyAAC. You can for example run code before the page has been generated, to inject some code into it. From the most importants, those are:

```
define('HOOK_STARTUP', 1); // executed after most of the AAC components has been initialized, so there is database connection, server status is checked and migrations are done.
define('HOOK_BEFORE_PAGE', 2); // before page will be included, can return false to omit page loading
define('HOOK_AFTER_PAGE', 3); // after page
define('HOOK_FINISH', 4); // last line of the index.php script, no other thing can be executed later ;)
```

and also:

```
define('HOOK_LOGIN', 13); // executed on succesfull login
define('HOOK_LOGIN_ATTEMPT', 14); // executed on unsuccesfull attempt
define('HOOK_LOGOUT', 15); // executed on logout
```

For other hooks look in:
* **system/hooks.php** (myaac 0.8)
* **system/src/global.php** (myaac 1.0+).
