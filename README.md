[![version](https://img.shields.io/badge/version-1.1.1-green.svg)](https://github.com/wizaplace/console-bundle)
[![symfony](https://img.shields.io/badge/symfony/symfony-^2.3%20||%20^3.0-blue.svg)](https://symfony.com)
![Lines](https://img.shields.io/badge/code%20lines-370-green.svg)
![Total Downloads](https://poser.pugx.org/wizaplace/console-bundle/downloads)

# ConsoleBundle

Allow to exclude some commands.

For example, if you don't want to have _doctrine:schema:update_ command in _prod_ env: now you can :).

Add configuration to _doctrine:schema:update_ to get queries for more than one database per connection.

[Changelog](changelog.md)

# Installation

```bash
composer require wizaplace/console-bundle ^1.1
```

```php
# app/AppKernel.php

class AppKernel
{
    public function registerBundles()
    {
        $bundles = [
            new \Wizaplace\ConsoleBundle\ConsoleBundle()
        ];
    }
}
```

# Exclude commands

You can exclude commands you don't need, or you don't want to be executed on this project / environment.

```php
# bin/console

# replace use Symfony\Bundle\FrameworkBundle\Console\Application; by this one
use Wizaplace\ConsoleBundle\Application;
```

Then configure commands you want to be excluded:
```yaml

# app/config/config.yml
console:
    excluded:
        - 'foo:bar:baz'
        - 'bar:foo:baz'
```

# doctrine:schema:update for more than one database

_doctrine:schema:update_ has a major problem for us: only one database per connection is managed.

In our projects, we have more than one database per connection, so _doctrine:schema:update_ don't show queries for all our databases.
 
_UpdateDatabaseSchemaCommand_ replace _doctrine:schema:update_, and call old _doctrine:schema:update_ for all configured databases!
 
```yaml
 
# app/config/config.yml
console:
    databases:
        - database_name_1
        - database_name_2
```
