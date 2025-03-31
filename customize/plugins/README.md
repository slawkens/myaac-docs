# Plugins

## Create new plugin

Go into `plugins` Create new file my-awesome-plugin.json

Paste

```json
{
	"name": "My Awesome Plugin",
	"description": "This is just an example of a Plugin for MyAAC.",
	"version": "1.0",
	"author": "YourNickname",
	"contact": "email@example.org",
	"require": {
		"myaac": "0.9.0",
	},
	"install": "plugins/my-awesome-plugin/install.php",
	"uninstall": [
		"plugins/my-awesome-plugin.json",
		"plugins/my-awesome-plugin"
	]
 }

```

Create directory `my-awesome-plugin`
