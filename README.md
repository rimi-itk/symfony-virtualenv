# symfony-virtualenv

Virtual environment for Symfony (<https://symfony.com/download>) to make it easy
to run `php` and `composer` (and other `php` based commands) without adding
`symfony` before each command, i.e. you can use

```sh
vendor/bin/drush
```

rather than

```sh
symfony php vendor/bin/drush
```

Usage:

```sh
# Activate by sourcing (don't run the script)
source activate
# Run your commands.
…
# Deactivate the virtual environment.
deactivate
```

## Supported commands

These commands will run in right symfony environment:

* `php` (cf. [bin/php](bin/php))
* `composer` (cf. [bin/composer](bin/composer))

`php` also works via `#!/usr/bin/env`, i.e. you can run `bin/console` directly
(rather than `php bin/console` or `symfony php bin/console`).

The `symfony` command is disabled in the virtual environment since running it
[may loop forever](https://en.wikipedia.org/wiki/Halting_problem).

## Tips and tricks

### Docker

Use symfony's [Docker
Integration](https://symfony.com/doc/current/setup/symfony_server.html#docker-integration)
for happy hacking.

### Drupal 8 and above

After running [`symfony
local:server:start`](https://symfony.com/doc/current/setup/symfony_server.html)
(either with `--daemon` or in another shell), run

```sh
export DRUSH_OPTIONS_URI=$(~/.symfony/bin/symfony run printenv SYMFONY_PROJECT_DEFAULT_ROUTE_URL)
```

`drush`, i.e. `vendor/bin/drush`, will now use the right site uri and
`vendor/bin/drush user:login` will sign you right into your local Drupal site.
