

Guide for installing Recipe
https://www.drupal.org/docs/extending-drupal/drupal-recipes

Repo Drupal Base Recipe
https://gitlab.com/kevinquillen/drupal-base

Composer based recipe guide
https://git.drupalcode.org/project/distributions_recipes/-/blob/1.0.x/docs/getting_started_d11.md

Clone Repo
`git clone git@github.com:renierjohn/drupal-recipe.git`

##
**For Docksal** 
settings.php (Docksal)
**Create settings.php** *(Can be skip / Will automatically create during site install)*
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
Install recipe via drush command from drupal core

    fin drush si minimal
    fin drush recipe core/recipes/standard

Install recipe via drush command from other recipe `kevinquillen/drupal-base`

    fin drush si minimal
    fin drush recipe ../recipes/drupal-base
##
**For standalone php (*must be version 8.3*)**

Permissions must follow to avoid issue:
-rw-r--r--  .ht.sqlite
-r--r--r--  settings.php

**Checkout to base branch**
`git checkout base`
`composer install
`
**Create settings.php** *(Can be skip / Will automatically create during site install)*
    
    $databases['default']['default'] = array (
      'database' => 'sites/default/.ht.sqlite',
      'prefix' => '',
      'driver' => 'sqlite',
      'namespace' => 'Drupal\\sqlite\\Driver\\Database\\sqlite',
      'autoload' => 'core/modules/sqlite/src/Driver/Database/sqlite/',
    );
    $settings['hash_salt'] = 'iLJgoqSV_g-6-NbwFtt9RDvB2Kr3VZwZRbXRVzwfZIsKMVZ_Uuf5MawmAxZy0copcCCqFrMbIA';
    $settings['config_sync_directory'] = 'sites/default/files/config_YKOUV2Ny2penQuPay3DP7eq_-nG4hDaT9ttU_wskyl6AdQ4BpiQNaUtxWf3KnQdPuruwTN0LzA/sync';

 Run site (Insure current dir is inside webroot)
`php -S localhost:8888 .ht.router.php`

How to run drush command *(Insure current dir is inside webroot)*
``../vendor/bin/drush``

How to Drop DB:
``../vendor/bin/drush sql:drop -y``

##
**Example 1 - Install Recipe from Drupal Core** 
2 methods to install recipe

A.) Installing recipe via Drupal script (Insure current dir is inside webroot)
```../vendor/bin/drush si minimal && php core/scripts/drupal recipe core/recipes/standard -v```

B.) Installing recipe via Drush command (Insure current dir is inside webroot)
````../vendor/bin/drush si minimal && ../vendor/bin/drush recipe core/recipes/standard````

##
**Example 2 - Install Recipe from other repo kevinquillen/drupal-base** 
Install composer plugin for Drupal Recipe:
``composer require oomphinc/composer-installers-extender``

Add VCS for kevinquillen/drupal-base recipe
  `{
     "type": "vcs",
     "url": "https://gitlab.com/kevinquillen/drupal-base"
    }`

Set installer path for recipe
`  "recipes/{$name}": ["type:drupal-recipe"]`
&

    "installer-types": ["drupal-recipe"],
    
Install drupal-base recipe:
 - `composer require kevinquillen/drupal-base`

Checkout to `feature-a` branch to see the new packages on composer.json
1. `git checkout feature-a`
2. `composer install`
3. Install drupal-base recipe
 `../vendor/bin/drush si minimal -y && ../vendor/bin/drush recipe ../recipes/drupal-base`

##
**Example 3 - Install Custom Recipe *(Added features from Example 2)*** 
Pre defined custom recipe in `feature-b` branch
Checkout to feature-b branch to see the custom-recipe
1. `git checkout feature-b`
2. `composer install`
 Install custom-recipe (Assuming feature-a already installed)
3. `../vendor/bin/drush recipe ../recipes/custom-recipe`

