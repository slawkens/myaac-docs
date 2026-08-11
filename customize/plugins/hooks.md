# Hooks

Hooks is an events system that allows you to customize AAC and inject code in places you want.

In this capitel the most important hooks will be listed.

Hooks need to be defined in plugin .json file.

Example:
```json
"hooks": [
	{
		"type": "HOOK_ADMIN_MENU",
		"file": "plugins/my-plugin/hooks/admin-menu.php"
	},
```

Type is hook name, and file is path to file on filesystem.

### HOOK_TWIG
Params: $twig, $twig_loader

This hook allows you to add custom functions to twig template engine.

This example adds a custom function.
```php
<?php
use Twig\TwigFunction;

$function = new TwigFunction('myFunction', function ($param1, $param2) {
	return $param1 . $param2;
});

$twig->addFunction($function);
```

Then in twig template, you use it:
```
{{ myFunction('Hello', 'World') }}
```

### HOOK_LOGIN
Params: $account (OTS_Account), $password, $remember_me (bool)

Executed after successful login. You can use it to add login history.

### HOOK_LOGIN_ATTEMPT
Params: $account (account name, number or id), $password, $remember_me

Executed after failed login attempt. You can add here custom logic to handle such cases - like a email notification or logging.

### HOOK_LOGOUT
Params: account_id (account id of the logging out account)

Executed after user logouts.

### HOOK_BEFORE_PAGE

Allows you to do custom stuff before page is loaded.
You can add here code that will be displayed above page.

If you return false in this hook, then the page won't be loaded. You can use it to display custom things.

This example will block every page and show instead a message: Hello World!

```php
<?php

echo 'Hello World!';
return false
```

### HOOK_ADMIN_MENU

This hook allows you to add/modify menus in admin panel.

This example adds "Gifts System" group with two links: Offers + Add Offer

```php
<?php
global $menus; // this is required to access array of menus

$menus[] = [
	'name' => 'Gifts System', 'icon' => 'gift', 'order' => 111, 'link' => [
		['name' => 'Offers', 'link' => 'gifts', 'icon' => 'list', 'order' => 10],
		['name' => 'Add Offer', 'link' => 'gifts&action=offer_form', 'icon' => 'plus', 'order' => 20],
	],
];
```

### HOOK_INSTALL_FINISH

Executed on the last page of the installation. Use if you have custom database changes you want to install.

### HOOK_EMAIL_CONFIRMED
Params: $account (OTS_Account)

Executed after user clicks link in email and confirms his email. Can be used to add custom rewards like items.

### HOOK_FILTER_TWIG_DISPLAY
### HOOK_FILTER_TWIG_RENDER
Params: $args['viewName']

Both can be used to pass custom parameters to $twig->display and $twig->render.

### HOOK_INIT
This is the first hook executed after the hooks system is initialized. There is no database connection yet.

### HOOK_STARTUP
Executed after all systems are loaded. The website is already connected to database, and login system is ready.

### HOOK_FINISH

This is the last executed hook, after that page is send to browser.