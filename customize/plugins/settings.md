# Settings

You can add your own settings to the admin panel.

For that, define following in your plugin .json file:

```json
"settings": "plugins/my-plugin/settings.php",
```

Now open plugins/my-plugin/settings.php and paste following, this is just a basic example:

```php
<?php

return [
	'name' => 'My Plugin', // name that will be displayed under Settings menu in Admin Panel
	'key' => 'my_plugin', // will be used with setting() function, must be unique for every plugin
	'settings' =>
	[
		[
			'type' => 'section',
			'title' => 'Section Name'
		],
		'enabled' => [
			'name' => 'Enable Something',
			'type' => 'boolean',
			'desc' => 'Enable something',
			'default' => false,
		],
		'type' => [
			'name' => 'ReCaptcha Version',
			'type' => 'options',
			'options' => ['v2-checkbox' => 'v2-checkbox', 'v2-invisible' => 'v2-invisible', 'v3' => 'v3'],
			'desc' => 'Type of ReCaptcha',
			'default' => 'v3',
			'show_if' => [
				'enabled', '=', 'true',
			]
		],
	]
];
```

Now you can access the settings in PHP by using function: `setting('key.option')`, example: `setting('my_plugin.enabled')`.

Following "type" are allowed:

### New Tab (category)
```php
[
	'type' => 'category',
	'title' => 'My Category Title'
],
```

### New Header (section)
```php
[
	'type' => 'section',
	'title' => 'My Section Title'
],
```

Note: After category, there is a requirement to add a section, otherwise it will not be displayed correctly.

### boolean (true/false)
```php
'csrf_protection' => [
	'name' => 'CSRF protection',
	'type' => 'boolean',
	'desc' => 'Its recommended to keep it enabled. Disable only if you know what you are doing.',
	'default' => true,
],
```

### number
```php
'smtp_port' => [
	'name' => 'SMTP Port',
	'type' => 'number',
	'desc' => '25 (default) / 587 (tls - GMail, Microsoft Outlook)',
	'default' => 25,
	'show_if' => [
		'mail_enabled', '=', 'true'
	]
],
```

### text (string)
```php
'google_analytics_id' => [
	'name' => 'Google Analytics ID',
	'type' => 'text',
	'desc' => 'Format: UA-XXXXXXX-X',
	'default' => '',
],
```

### textarea (long text)
```php
'meta_keywords' => [
	'name' => 'Meta Keywords',
	'type' => 'textarea',
	'desc' => 'keywords list separated by commas',
	'default' => 'free online game, free multiplayer game, ots, open tibia server',
]
```

### options (select)
```php
'cache_engine' => [
	'name' => 'Cache Engine',
	'type' => 'options',
	'options' => ['auto' => 'Auto', 'file' => 'Files', 'apc' => 'APC', 'apcu' => 'APCu', 'disable' => 'Disable'],
	'desc' => 'Auto is most reasonable. It will detect the best cache engine',
	'default' => 'auto',
],
```
