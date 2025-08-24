# Commands

## About

The CLI interface to interfere with myaac is called: __aac__

It's php file like in Laravel there is __artisan__.

The whole concept is based on the Symfony component - Console. You can find a lot of documentation and how to write commands on their website - https://symfony.com/doc/current/components/console.html

How to use that? Just write in console (while being in myaac main folder): `php aac` - you should see a list of commands.

I will also try to summarize in this document available commands.

### List

Prefix each command with `php aac`, like `php aac cache:clear`

* cache:clear

  Clears the cache

* cronjob

  Runs the cronjob tasks, defined inside the HOOK_CRONJOB hook

* cronjob:install

  Installs the cronjob script into crontab. It's like manually editing the cronjob using command: `crontab -e` and adding the line for every minute

* mail:send --subject="{your-subject}" {recipient}

  Sends a mail to specified user.

  * Options:
    * --subject="{your-subject}"

  * Arguments:
    * {recipient} The recipient can be specified as: email, account name, or player name.

  * Example usage:
    * echo "Hello World" | php aac email:send --subject="This is the subject" user@domain.com

* migrate

  Runs migrations up to the latest one. Not required if "Database Auto Migrate" is enabled in Settings, which is the default.

* migrate:run {id or ids}

  Runs a migration(s) specified by the argument. Can be either id or list of ids. List of ids should be separated by space. This one is wild, because it doesn't change the database_version in config. Advised is to use just `migrate` or `migrate:to`, instead of this one. Run if you know what you're doing!

  * Options:
    * --down (perform downgrade instead of upgrade)

  * Arguments:
    * {id or ids}

  * Example usage:
    * php aac migrate:run 34 35 36 (Runs migrations 34, 35 and 36)
    * php aac migrate:run --down 36 35 34 (run downgrades of 36, 35, and 34)

* migrate:to {version}

  This one migrate from current version, to the selected {version}. It auto-detects if it's downgrade or upgrade, so the version can be either lower or higher.

  * Arguments:
    * {version} To which version should we migrate

  * Example usage:
    * php aac migrate:to 37 (downgrade to 37 version of database)
    * php aac migrate:to 45 (upgrade to 45)

* plugin:install {path-to-plugins-zip-file}

  Installs a plugin specified by path. Exactly the same as installing from admin panel.

  * Arguments:
    * {path-to-plugins-zip-file} Full path to the plugin .zip

  * Example usage:
    * php aac plugin:install "/home/user/myaac-powergamers-v1.0.zip"

* plugin:setup {plugin-name}

  Executes the setup/install part of the plugin. It's supposed to do required database changes/installing new tables etc.

  * Aliases (previously known as)
    * plugin:install:install (renamed in 1.7.1)

  * Arguments:
    * {plugin-name} Name of the plugin as specified in the .json name.
      * For the gesior-shop-system.json, it will be just "gesior-shop-system"

  * Example usage:
    * php aac plugin:setup gesior-shop-system
    * php aac plugin:install:install gesior-shop-system
      * Doing exactly the same, just an alias of old name of the command

* settings:reset {plugin-name}

  Resets the settings for the specified plugin, or all settings if {plugin-name} is not specified.

  * Arguments:
    * {plugin-name} - optional, plugin settings to reset, if not specified, then all settings will be cleared

  * Example usage:
    * php aac settings:reset
      * Resets all MyAAC settings
    * php aac settings:reset google-recaptcha
      * Resets only google-recaptcha settings

* settings:set {name.key} {value}

  Change/set setting specified by key.

  * Arguments:
    * {name.key} Name of the settings + key, can be also plugin-name + key.

  * Example usage:
    * php aac settings:set core.template kathrine
    * php aac settings:set core.template_allow_change false
      * Those both change the default template, and doesn't allow to change it by user


### Extending

You can add your own commands using plugins. Just create a new folder in your plugin folder called: __commands__.

Create file HelloWorldCommand.php and paste inside:
```
<?php

namespace MyAAC\Commands;

use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;
use Symfony\Component\Console\Style\SymfonyStyle;

return new class extends Command
{
	protected function configure(): void
	{
		$this->setName('hello:world')
			->setDescription('Description');
	}

	protected function execute(InputInterface $input, OutputInterface $output): int
	{
		$io = new SymfonyStyle($input, $output);

		$io->success('Hello world!');
		return Command::SUCCESS;
	}
};
```

Now after using `php aac hello:world` you should see a message.