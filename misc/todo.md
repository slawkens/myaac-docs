# TODO

## MyAAC TODO

This is a list of things that are planned for MyAAC. Everyone is welcome to pick anything, implement it, and then create a PR (Pull Request).

Please follow some basic rules

### High Priority (ASAP)

#### There is problem with finding config.lua on linux

It's a problem with permissions file\_exists(config.lua) returns false, even though the file exists

The current solution is to set execute flags on every folder above ots path So if your config.lua (server) is located in: /home/myuser/forgottenserver/config.lua, then you need to execute following commands:

```
chmod +x /home
chmod +x /home/myuser
chmod +x /home/myuser/forgottenserver
```

And then refresh the installation page again and follow the instructions.

And here's the list:

* automatic updater of the AAC files (like in WordPress)
* use separate tables without modifing the OTServ schema (myaac\_accounts, myaac\_players)
* fundamental changes in Twig:
  * add option to write themes in Twig
* better gallery with carousel
  * that is automatically generated from images in images/gallery folder (no need to upload)
* flags/permissions editor as new tab in accounts editor
  * example flag (for reference): FLAG\_CONTENT\_MAILER
  * after done: remember to remove "Website Access:" from account tab
* maybe we can move serverInfo page to database (Pages) so it can be edited in Admin Panel (check how far possible)
* move gallery Class to libs/gallery.php
* kathrine tickets - show/hide
* change constants: BASE\_URL to base\_url(), USE\_ACCOUNT\_NAME to config
* new configurables:
  * login\_session\_time
  * login\_fail\_attempts
  * login\_fail\_attempts
  * account\_identity = name,number,email
* move website from WordPress to github.io or readthedocs.org
* WordPress: Insert Headers and Footers
  * nice example how to insert to head, body from Admin Panel
  * can be used to insert Google Analytics tags, HotJar, etc.
* plugin auto-update and check-version
  * needs support from my-aac.org (plugins database)
* configurable session handler: file, database, php
* change global variables pointing to classes like $db, $cache to Singleton Pattern
* new command to install the AAC from command line
  * headless install
* i18n support (issue #1 on GitHub)
  * use some web-based translation tools
    * most preferably https://weblate.org
    * or: [https://crowdin.com/](https://crowdin.com/)
* extend forum
  * use avatars or player outfits (configurable)
  * colorful nicknames for different groups
  * profile page
    * change signature
    * update avatar
  * member since (in forum post)
  * better looking pagination (bootstrap) + configurable for each template (look: laravel)
  * go to the last post
  * select icon for the topic
  * forum - thread name instead of id in URL
* remove all copy-writed content

## x.x - At any time between (version not specified)

* better news archive with search function (like on the original game website)
* new lostaccount interface
  * that allows recover by email address
  * look on original game website, they got something there
* Export list of plugins as .json or .txt
* server data editor (web based file manager that shows and allows to edit the data folder)
* configurable items storage -> db (slower load\&parse, better search) vs cache (faster load\&parse, worse search)
* better looking email templates
* Achievements System

## Plugin Ideas

* First 100 (x) accounts receive points/pacc
  * limit per IP

## Template Ideas

* add support for menus/color/blank in rest of templates
* https://vikpe.org/archive/arcsin-web-templates/demo/beautiful-day-website-template/
* https://templates.arcsin.se/demo/fluid-solution-website-template/
* https://templates.arcsin.se/demo/transparentia-website-template/
* http://www.css3templates.co.uk/templates/CSS3\_skies/index.html
