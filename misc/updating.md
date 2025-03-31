# Updating

Updating AAC to the newest version is very simple. Thanks to our migration script your database schema will be automatically updated when first time visiting the updated site.

To easily update your AAC without conflicts, please use config.local.php to store your config.php changes. This way you won't need to care about config changes that were applied between releases.

## How to use config.local.php?

Copy config value from config.php, and paste it into config.local.php into $config array.

Example: (if you want to modify friendly\_urls from config.php)

Content you need to paste into config.local.php would be then (example):

`$config['friendly_urls'] = true;`

## How to update MyAAC?

1. Download chosen version of MyAAC here: https://github.com/slawkens/myaac/releases
2. Unpack it somewhere, lets say **MyAAC-dir**.
3. Copy config.local.php from your old MyAAC installation to some safe place.
4. Copy content of **MyAAC-dir** to your MyAAC installation directory, replace all files.
5. Copy your config.local.php that you saved before to your MyAAC installation directory, replace the old one.
6. Install plugins that you had activated before. You can do this with our command line php script. (To be explained)
