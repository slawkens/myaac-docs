# Templates

## Create new template

So you want to create a template for MyAAC? That's pretty straightforward!

Templates are placed under **templates/** folder in the MyAAC installation.

> Notice: there is also _system/templates_ folder, that serves for different purposes. It is used for HTML Twig templates. Let's distinguish between those two

This tutorial is targeted against version 0.8 and higher of MyAAC. It won't work with 0.7, because there were some incompatibilities being introduced between the releases, like now you use `config('key')` function instead of the global variable `$config['key']`.

### Naming convention

Your main template file where header, footer and content (generally whole HTML structure) are stored should be named **index.php**. And it should be placed inside your template folder like this: _templates/example/index.php_, where _example_ is your template name.

Images can be placed into _templates/example/images_ but that's up to you how you name the folder. Same with CSS and JavaScript, it's up to you where you place them.

### Protect the script

At the beginning of your template index.php file add this:

```php
<?php
defined('MYAAC') or die('Direct access not allowed!');
?>
<!DOCTYPE html>
<html>
...
```

This protects the script from being directly accessed by browser.

### Configuration (config.ini & config.php)

If you have something that you want to make for the users configurable, you can place it in **config.ini** or **config.php** of your template folder.

> If you want your template to be compatible with **MyAAC 0.7** and lower, then you need to either create config.ini or config.php, both cannot exist cause they won't be loaded by MyAAC!

Syntax of ini is very easy (simple key=value). And its being internally parsed by PHP function [parse\_ini\_file](https://www.php.net/manual/en/function.parse-ini-file.php)

Example of config.ini

```ini
darkborder = "#D4C0A1"
lightborder = "#F1E0C6"
vdarkborder = "#505050"

logo_monster = "Wyrm"
```

Then in your template (index.php) you can use for example:

```php
<?php echo config('logo_monster'); ?> // since 0.8
```

Or:

```php
<?php echo $config['logo_monster']; ?> // 0.7 and older (for compatibility)
```

### Content

Now we came to the most visible part of the page. Content.\
Content is something that dynamically changes between pages. Create account, highscores and downloads page are examples of content.

To place this content on your website use the `$content` variable in your template.

Example:

```php
<div class="panel panel-default">
    <div class="panel-body">
        <?php echo template_place_holder('center_top') . $content; ?>
    </div>
</div>
```

As wrote, `$content` will be dynamically generated with every page refresh and will include the main content of the page.

### Placeholders

MyAAC automatically generates some HTML code for your template to make it easier to develop plugins that can automatically inject code into it. This is:

* META tags (like title, charset, content-language, description and keywords based on configuration)
* jQuery, ReCaptcha and other JavaScript tags
* some CSS stuff

Like wrote, jQuery is automatically included with every template that includes placeholders, so you don't need to include it in your script.

There are 3 place holders that are mandatory (without them your template won't work correctly). Those are: `head_start`, `head_end` and `body_end`.

To include placeholder in your template, just use following PHP Code:

```php
  <?php echo template_place_holder('here_the_name'); ?>
```

Placeholders needs to be located in following places:

* `<?php echo template_place_holder('head_start'); ?>` just after opening `<head>`
* `<?php echo template_place_holder('head_end'); ?>` just before closing `</head>`
* `<?php echo template_place_holder('body_end'); ?>` just before closing `</body>`

#### Optional placeholders

Some optional placeholder is `center_top`.

Its used for example by the plugins [Welcome Box](https://otland.net/threads/myaac-welcome-box-last-joined-best-player-total-houses.268583/) or [Powerful guilds](https://otland.net/threads/myaac-plugin-most-powerful-guilds-tfs-0-3-4-and-1-0.254708/). Plugins can inject here some code that will be displayed just before the `$content`.

Its typical to mix them in one line, so usually you should have something like this:

```php
<?php echo tickers() . template_place_holder('center_top') . $content; ?>
```

### Status

You may wish to add status of the server to your template. For this, you can use the `$status` variable.

Example:

```php
if(!$status['online']) {
	echo 'Offline!';
}
else {
	echo 'Online!';
}
```

Except that, you can use following array-keys:

```php
<?php
echo ($status['online'] ? 'Online' : 'Offline');
echo $status['players']; // number of players online
echo $status['playersMax']; // maximum number of allowed players
echo $status['lastCheck']; // timestamp of the last status check
echo $status['uptime']; // uptime in seconds
echo $status['uptimeReadable']; // uptime formatted (example: **1h 25m**)
echo $status['monsters']; // amount of monsters on server
echo $status['motd']; // motd

echo $status['mapAuthor'];
echo $status['mapName'];
echo $status['mapWidth'];
echo $status['mapHeight'];

echo $status['server'];
echo $status['serverVersion'];
echo $status['clientVersion'];
?>
```

> Notice: Some of these variables are available only if the server is online (`$status['online'] = true`), so you need to check the status first before using them.

### Functions

In your template you can use some helper functions that are specially made for templates.

#### config(key), configLua(key)

Get config option from MyAAC config, or from server .lua file.

> Notice: only MyAAC 0.8 and higher

Example:

```php
<?php
echo configLua('serverName'); // outputs **Forgotten Server**
echo config('server_path'); // outputs **/home/otsmanager/forgottenserver/**
?>
```

#### getLink(name)

Use it to generate links to your pages.

Example:

```php
<li><a href="<?php echo getLink('account/manage'); ?>">My Account</a></li>
<li><a href="<?php echo getLink('creatures'); ?>">Creatures</a></li>
```

#### template\_form()

Use it to place a form on the page where user can change template. Its good practice to make it configurable.

Example:

```php
<?php
    if($config['template_allow_change']) {
        echo '<span style="color: white">Template:</span><br/>' . template_form();
    }
?>
```

#### template\_footer()

Use it to place auto-generated footer on the website. It includes page load time, visitors, copyright notices and famous "Powered by MyAAC." text.

Example: (taken from ShadowCores templates)

```php
    <div class="panel panel-default">
        <div class="panel-heading" style="text-align: center;">
            <?php echo template_footer(); ?><br/>
            <b>Template by:</b> <a href="https://otland.net/members/webo.192791/" target="_blank">Webo</a>.
        </div>
    </div>
```

#### getTopPlayers($amount)

Use it go get top players of the server, wherever you can specify $amount yourself. This function automatically caches the result, so you don't need to care about performance.

Example:

```php
<?php
	$count = 1;
	foreach(getTopPlayers(5) as $player) {
		echo "<li>$count - <a href='"getPlayerLink($player['name'], false). "'>". $player['name']. "</a> <span style='float:right; font-size: 12px; padding-right: 5px;'>Level: ". $player['level'] ."</span></li>";
		$count++;
	}
?>
```

#### tickers()

Use it to place the tickers on the page.

Example:

```php
<?php echo tickers() . template_place_holder('center_top') . $content; ?>
```

For more functions look into [system/functions.php](https://github.com/slawkens/myaac/blob/master/system/functions.php)

### Tipps

#### Display server IP/domain:

For displaying server IP or domain you can use PHP built-in variable `$_SERVER['SERVER_NAME']`;

Example:

```php
IP: <?php echo $_SERVER['SERVER_NAME']; ?>
```

#### Display client version:

Use `$config['client']` divided by 100.

Example:

```php
Client: <?php echo ($config['client'] / 100); ?>
```

#### Display images or include style/javascript to your template folder.

If you place files under your template folder, you can refer to them with the `$template_path` variable.

Normally, you would do it like this:

```php
<img src="templates/example/background.jpg" alt="background"/>
```

But imagine, if you change the name of your template from **example**, to something else, like **example2**.

Then you will need to replace all templates/example in your template! That's may introduce a lot of useless work!

For this, you can use built-in `$template_path` variable.

So, instead do this this way:

```php
<img src="<?php echo $template_path; ?>/background.jpg" alt="background"/>
```

Do same, with including javascript:

```php
<script src="<?php echo $template_path; ?>/js/bootstrap.min.js"></script>
```
