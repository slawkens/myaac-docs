# Compatibility

Here's a list of biggest changes in structure and functions of MyAAC that may require you to define in your plugin manifest json file different minimal MyAAC version to be supported.

You can define the minimum version on which MyAAC plugin can be installed like this: (in your .json file)

```
"require": {
	"myaac": "0.4.3"
},
```

## Versions:

### v0.3.0

* added Twig template engine

### v0.4.0

* Automatically detect json file in .zip instead of basing on filename (admin panel - plugins installer)

> in this update your plugin json file doesn't need to have anymore the same name as .zipped file. Like my-plugin.zip, then plugin.json location should be plugins/my-plugin.json. From now you can use custom names like my-plugin.zip and plugins/another-name-for-this.json. We still however, advice you to use same name of plugin like the name of .zip file to support older MyAAC versions.

### v0.5.0

* moved .htaccess rules to plain php (index.php)

> This adds new addresses like /account/manage or /account/create

* added option to uninstall plugin
* added option to require specified myaac, php or database version for plugins, without that plugin won't be installed
* added admin panel custom links support - for future plugins. You can hook you menus on plugin install into `myaac_admin_menu` table

### v0.6.1

* new configurable: session\_prefix, to allow more websites on one machine (must be unique for every website on your dedicated server!

> You should be using now functions: getSession(key) and setSession(key, value) for dealing with user session data. This way session\_prefix will be automatically appended to the session name.

### v0.6.2

* added forums for guilds and groups
* added items.xml loader class and weapons.xml loader class, they're now saved in database, and you can use them in your plugin

### v0.7.0

* moved template menus to database, they're now dynamically loaded

### v0.8.0

* Admin Panel - Modules showed on Dashboard - for example can be statistics
* colorful Menus:

> possibility to define colors and "Open in New Tab" on Template Menus (needs to be supported by Template)

* new configurable: "env" (Environment)
* comments are now allowed inside plugin json file (php style)
* new require options for plugins: (look into example.json)
  * require database version, table or column of the MyAAC schema
  * require php-extension
* new hooks: LOGIN, LOGIN\_ATTEMPT, LOGOUT, HOOK\_ACCOUNT\_CREATE\_\*
* $cache variable was removed, use `$cache = Cache::getInstance()` instead
* new functions:
  * config($key), configLua($key)
  * clearCache()
  * OTS\_Account:
    * getCountry()
    * setLastLogin($lastlogin) (@Leesneaks)
    * setWebFlags(webflags) (@Leesneaks)
  * OTS\_Player:
    * getAccountId()
    * countBlessings() (@Leesneaks)
    * checkBlessings($count) (@Leesneaks)
  * is\_sub\_dir (in system/libs/plugins.php)
  * Twig:
    * getPlayerLink($name, $generate = true)
  * removed SQLquote and SQLquery from OTS\_Base\_DB
  * Add optional $params param into log\_append (will log arrays)

### v0.8.8

* Change PHP Required: 7.2.5
* updated Twig from version 1.x to 2.x (v2.15.4)
* New hook:
  * HOOK\_EMAIL\_CONFIRMED

### v0.8.9

* add PLUGINS dir to twig paths

> you can now include twig template inside your plugins folder `$twig->display('your-plugin/example.html.twig');`

* plugins folder is now accessible from public, you can place assets there
* added tables.headline.html.twig

### v0.8.10

* allow pages to be placed in templates folder

### v0.8.11

* New functions:
  * Cache::remember($key, $ttl, $callback)
* New characters page hooks
  * HOOK\_CHARACTERS\_BEFORE\_SKILLS
  * HOOK\_CHARACTERS\_AFTER\_SKILLS
  * HOOK\_CHARACTERS\_AFTER\_QUESTS
  * HOOK\_CHARACTERS\_AFTER\_EQUIPMENT
  * HOOK\_CHARACTERS\_BEFORE\_DEATHS

### v0.8.13

* Twig context for hooks - this way you can get variables from parent template in hooks

### v0.8.17

* TwigTypeCastingExtension (https://github.com/slawkens/myaac/commit/7181b988e9518320d57486670ca4e2d3b2fe1cfa)
* can be used to cast variables in Twig

### v0.8.18

* Added hook: HOOK\_GUILDS\_AFTER\_INVITED\_CHARACTERS for Guild Wars

### v0.8.19

* better tables.headline.html.twig (patched from 1.0)&#x20;
* new functions: getGuildNameById($id) + getGuildLogoById($id) + Plugins::installMenus($templateName, $menus, $clearOld = false)
* new hooks: HOOK\_ACCOUNT\_CREATE\_AFTER\_SAVED, HOOK\_ACCOUNT\_MANAGE\_BEFORE\_GENERAL\_INFORMATION, HOOK\_ACCOUNT\_MANAGE\_BEFORE\_PUBLIC\_INFORMATION, HOOK\_ACCOUNT\_MANAGE\_BEFORE\_ACCOUNT\_LOGS, HOOK\_ACCOUNT\_MANAGE\_BEFORE\_CHARACTERS, HOOK\_INSTALL\_FINISH, HOOK\_ACCOUNT\_CREATE\_CHARACTER\_\*
* syntactic sugar for db structure changes (https://github.com/slawkens/myaac/commit/e0036a3e32e8c37c28665dd7ae18ac9b8fc167d9)
* support for button\_color (red, green, blue) in buttons.base.html.twig (https://github.com/slawkens/myaac/commit/b2c9eb474513650a014352d820602b8007eb3bf3)

### v1.0 (current stable, main branch)

* new pages, commands and themes can be placed directly in plugins folder. The respective folder are following:
  * You need just to place them in correct folder, and they will be loaded automatically - this allows better customization, without interfering with core AAC folders. This will allow in the future automatic updates for plugins as well the AAC as whole.
    * pages/
    * commands/
    * themes/
      * autoload of pages, commands and themes is configurable (https://github.com/slawkens/myaac/commit/c1d4b4f80cd6bb85507ee9471e47013955a26a91)
* composer is now used for external libraries
* new console script: aac - using symfony/console
  * usage: `php aac` (will list all commands by default)
  * example: `php aac cache:clear`
  * example: `php aac plugin:install theme-example.zip`
* Plugin cronjobs: central control of the cronjobs
* New exception handler: Whoops
* replace POT Query Builder to Eloquent ORM
* config.php moved to Admin Panel -> Settings page
* schema: Change character set to utf8mb4 (support for Emojis in Menus/Pages/News/Forum etc.)
* allow OTS\_Player to be passed as object to getPlayerLink
* refactor getTopPlayers function (support for balance)
* Bugtracker has been moved to Plugins
* new routing engine. Routes can be added to plugins. Thus removing the need of inserting the page into system/pages.

```json
"routes": {
	"First Route": {
		"pattern": "/YourAwesomePage/{name:string}/{page:int}",
		"file": "plugins/your-plugin/your-awesome-page.php",
		"method": "GET",
		"priority": "130"
	},
	"Redirect Example": {
		"redirect_from": "/redirectExample",
		"redirect_to": "account/manage"
	}
}
```

* option to disable/enable plugin from admin panel
* templates: new config option - menu\_default\_color
* add $whoopsHandler as variable
* new hooks for news management (https://github.com/slawkens/myaac/commit/011a85d8ae34283ded6999882833f9d4797028ec, https://github.com/slawkens/myaac/commit/36bd3eb846e829b45313e10f7568dc4e95841143)
* new functions
  * getBanReason($reasonId), getBanType($typeId)
  * getChangelogType($v), getChangelogWhere($v)
  * getPlayerNameByAccount($id)
  * Outfits\_loadfromXML(), Mounts\_loadfromXML()
  * left($str, $length), right($str, $length), between($x, $lim1, $lim2), truncate($string, $length)
  * getCreatureImgPath($creature), getItemRarity($chance)
  * getAccountLoginByLabel()
  * getGuildNameById($id), getGuildLogoById($id)
  * camelCaseToUnderscore($input), removeIfFirstSlash(&$text)

### v1.0.1

* Updated libs:
  * twig from ^2.0 to ^3.11
    * The "if" statements in "for" loops are not allowed anymore, this will cause an exception
  * tinymce from ^6.8.3 to ^7.2.0
  * cypress from ^12.12.0 to ^13.17.0
  * nesbot/carbon from 2.72.5 to 2.72.6

### v1.2
* Add HOOK_INIT, executed just after $hooks are loaded
* Twig:
  * Add template_name to twig variables
  * Add session(key) function + reworked session functions to accept multi-array like in Laravel
* Settings: password input hide/show, for sensitive data like API keys
* Rework menus: Different categories can have different colors + Option to reset menus

### v1.4
* Plugins:
  * json: Plugin name is required, a version is optional now
  * Feat: admin-pages (can add admin pages through plugins) (https://github.com/slawkens/myaac/commit/ceaa0639e66d31e8177ff90791463470367aa45d)
* Functions:
  * db->hasTableAndColumns(table, columns)
* Twigs: Add noSubmit option to buttons.base

### v1.5
* Twig:
  * Filter hooks: https://github.com/slawkens/myaac/pull/258
  * Add db variable to twig
  * Possibility to use a custom **views/** folder in the themes for twigs, for better organization
* Settings:
  * Add float and double types

### v1.7
* Plugins:
  * Add version check from plugins repo API
* New hooks:
  * HOOK_ACCOUNT_MANAGE_AFTER_CHARACTERS
  * HOOK_GUILDS_AFTER_MANAGE_BUTTON

### v1.8.1
* New Commands:
  * plugin:enable/disable/uninstall {plugin-name}

### v1.8.2
* Routes: 
  * Possibility to override routes with plugins pages, like characters.php - No need to define routes in plugin.json anymore

### v1.8.3
* New config:
  * hooks_debug (To view where hooks are located in .twig files), set it to true in config.local.php to activate it
* New Functions: 
  * db->getColumnInfo(table, column)
* Router:
  * Add an option to use ?subtopic=page-name for pages loaded by plugins (easier migration from 0.8.x)
* getTopPlayers() Function - Add lookmount & promotion
* New hooks:
  * HOOK_ACCOUNT_CHANGE_PASSWORD_AFTER_OLD_PASSWORD
  * HOOK_ACCOUNT_CHANGE_PASSWORD_AFTER_NEW_PASSWORD
* Cache::remember $ttl = -1 = infinite

### v1.8.5
* Settings: escapeHtml in values (support for HTML code)
* Plugins System: Add plugin:remove + plugin:delete as alias for plugin:uninstall + plugin:activate/deactivate

### v1.8.6
* New hook for validate character name:
  * HOOK_FILTER_VALIDATE_CHARACTER_NEW_NAME

### v1.8.8
* Twig: Extract $twig→renderInline(content, context) as a method
* Settings: Fix variable overlapping if the same var name as in core
  * You can use a variable called env or anything you wish
* New hooks for the change-comment page:
  * HOOK_ACCOUNT_CHARACTERS_CHANGE_COMMENT_AFTER_SUCCESS
  * HOOK_ACCOUNT_CHARACTERS_CHANGE_COMMENT_AFTER_NAME
  * HOOK_ACCOUNT_CHARACTERS_CHANGE_COMMENT_AFTER_HIDE_ACCOUNT
  * HOOK_ACCOUNT_CHARACTERS_CHANGE_COMMENT_AFTER_COMMENT

### v2.0-dev (development version)
* Add the possibility to fetch skills, balance and frags in the getTopPlayers function (#347)
* Reworked account action logs to use a single IP column as varchar(45) for both ipv4 and ipv6 (#289)