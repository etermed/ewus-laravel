# Laravel eWUŚ

This package is Laravel wrapper for [nextgen-tech/ewus](https://github.com/nextgen-tech/ewus-php) package.

## Requirements

| Version | Laravel | PHP    |
| ------- | ------- | ------ |
| 1.x     | >= 6.0  | >= 7.3 |

## Installation

```sh
composer require nextgen-tech/ewus-laravel
```

Next run artisan command to set current password to eWUŚ:

```sh
php artisan ewus:password --init
```

## Configuration (.env)

### Base

* **EWUS_SANDBOX_MODE** (*default: false*) - disables/enables sandbox mode
* **EWUS_CONNECTION** (*default: http*) - connection used for communication

### Connection

* **EWUS_CONNECTION_TIMEOUT** (*used only by http connection*) - duration to timeout request, in seconds

### Password

* **EWUS_PASSWORD_LENGTH** (*default: 8*) - random generated password length

### Credentials

* **EWUS_CREDENTIALS_DOMAIN** - operator domain
* **EWUS_CREDENTIALS_LOGIN** - operator login
* **EWUS_CREDENTIALS_OPERATOR_ID** (*default: null*) - operator identificator, required only for certain domains
* **EWUS_CREDENTIALS_OPERATOR_TYPE** (*default: null*) - operator type, required only for certain domains

## Scheduling password changes

eWUŚ requires password changes every two weeks. We recommend changing it more frequently to be sure it will not expire. To automate this process you can create schedule which will call artisan command:

```php
// app/Console/Kernel.php

protected function schedule(Schedule $schedule)
{
    // other schedules

    $schedule->command('ewus:password --random')->weeklyOn(1, '00:00');
}
```