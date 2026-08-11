# Admin Pages

You can place your own admin pages.
They will be accessible under `/admin`, specifically `/admin/?p=your-page-name`.

Create a file `your-page-name.php` in the `plugins/my-plugin/admin-pages` directory.

```php
<?php
defined('MYAAC') or die('Direct access not allowed!');

$title = 'My Admin Page';

if (isset($_POST['submit'])) {
	// do something with the form data
}

success('Hello from my admin page!');

// display something
$twig->display('your-page-name.html.twig');
```

Now head to admin/?p=your-page-name to see the page live.

You can also add the link to this page in the admin panel.

For that, use the HOOK_ADMIN_MENU.

Example: (plugins .json)
```json
"hooks": [
	{
		"type": "HOOK_ADMIN_MENU",
		"file": "plugins/my-plugin/hooks/admin-menu.php"
	},
```

plugins/my-plugin/hooks/admin-menu.php:
```php
<?php
global $menus; // this is required to access array of menus

$menus[] = [
	'name' => 'My Page', 'icon' => 'gift', 'order' => 111, 'link' => 'your-page-name',
	],
];
```

