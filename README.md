Guide for installing Recipe
https://www.drupal.org/docs/extending-drupal/drupal-recipes

Repo Drupal Base Recipe
https://gitlab.com/kevinquillen/drupal-base


git clone 

settings.php (Docksal)
````
<?php

$databases['default']['default'] = array (
  'database' => 'default',
  'username' => 'user',
  'password' => 'user',
  'prefix' => '',
  'host' => 'db',
  'port' => '3306',
  'isolation_level' => 'READ COMMITTED',
  'driver' => 'mysql',
  'namespace' => 'Drupal\\mysql\\Driver\\Database\\mysql',
  'autoload' => 'core/modules/mysql/src/Driver/Database/mysql/',
);
$settings['hash_salt'] = 'iLJgoqSV_g-6-NbwFtt9RDvB2Kr3VZwZRbXRVzwfZIsKMVZ_Uuf5MawmAxZy0copcCCqFrMbIA';
$settings['config_sync_directory'] = 'sites/default/files/config_dB3xAjgpxxUMak2CYkf3dtpJ19NpcaOizV32qbVLFKSKzyQcE2uJ0jJfWGzFxZU9NevUAcGP7w/sync';
```
````
Installing recipe via drush
`fin drush recipe core/recipes/standard`




sqlite (standalone php)
-rw-r--r--  .ht.sqlite
-r--r--r--  settings.php
    
    $databases['default']['default'] = array (
      'database' => 'sites/default/.ht.sqlite',
      'prefix' => '',
      'driver' => 'sqlite',
      'namespace' => 'Drupal\\sqlite\\Driver\\Database\\sqlite',
      'autoload' => 'core/modules/sqlite/src/Driver/Database/sqlite/',
    );
    $settings['hash_salt'] = 'iLJgoqSV_g-6-NbwFtt9RDvB2Kr3VZwZRbXRVzwfZIsKMVZ_Uuf5MawmAxZy0copcCCqFrMbIA';
    $settings['config_sync_directory'] = 'sites/default/files/config_YKOUV2Ny2penQuPay3DP7eq_-nG4hDaT9ttU_wskyl6AdQ4BpiQNaUtxWf3KnQdPuruwTN0LzA/sync';
Running site (Insure current dir is inside webroot)
`php -S localhost:8888 .ht.router.php`

Running drush (Insure current dir is inside webroot)
``../vendor/bin/drush``

Installing recipe via Drupal script (Insure current dir is inside webroot)
```../vendor/bin/drush si minimal && php core/scripts/drupal recipe core/recipes/standard -v```

Installing recipe via Drush command (Insure current dir is inside webroot)
````../vendor/bin/drush si minimal && ../vendor/bin/drush recipe core/recipes/standard````

Drop DB
``../vendor/bin/drush sql:drop -y``


Composer based recipe guide
https://git.drupalcode.org/project/distributions_recipes/-/blob/1.0.x/docs/getting_started_d11.md

Installing composer plugin for Drupal Recipe
``composer require oomphinc/composer-installers-extender``

Add VCS for kevinquillen/drupal-base recipe
  `{
     "type": "vcs",
     "url": "https://gitlab.com/kevinquillen/drupal-base"
    }`

Set installer path for recipe
`  "recipes/{$name}": ["type:drupal-recipe"]`

      `  "installer-types": ["drupal-recipe"],`


Install drupal-base recipe
`../vendor/bin/drush si minimal -y && ../vendor/bin/drush recipe ../recipes/drupal-base`
