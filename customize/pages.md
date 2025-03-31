# Pages

## Create new page

### Through filesystem

Go into `system/pages` Create new file called my-awesome-page.php

Paste this

```php
<?phpp
defined('MYAAC') or die('Direct access not allowed!');
$title = 'My Awesome Page';

echo 'This is my awesome page';
// edit your page content
```

Visit http://localhost/?p=my-awesome-page to view the page.

### Through admin panel

Go to `localhost/admin`

Go to `Pages` -> `Add`

Check "Enable TinyMCE"

Now with the visual editor you can edit the page look.

You can also check "PHP" and paste PHP page in the editor.
