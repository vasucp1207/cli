# Utopia CLI

[![Build Status](https://travis-ci.org/utopia-php/cli.svg?branch=master)](https://travis-ci.org/utopia-php/cli)
![Total Downloads](https://img.shields.io/packagist/dt/utopia-php/cli.svg)
[![Chat With Us](https://img.shields.io/gitter/room/utopia-php/community.svg)](https://gitter.im/utopia-php/community?utm_source=share-link&utm_medium=link&utm_campaign=share-link)

Utopia framework CLI library is simple and lite library for extending Utopia PHP Framework to be able to code command line applications. This library is aiming to be as simple and easy to learn and use.

Although this library is part of the [Utopia Framework](https://github.com/utopia-php/framework) project it is dependency free and can be used as standalone with any other PHP project or framework.

## Getting Started

Install using composer:
```bash
composer require utopia-php/cli
```

script.php
```php
<?php

require_once '../vendor/autoload.php';

use Utopia\CLI\CLI;
use Utopia\CLI\Console;
use Utopia\Validator\Email;

$cli = new CLI();

$cli
    ->task('build')
    ->param('email', null, new Email())
    ->action(function ($email) {
        Console::success($email);
    });

$cli->run();

```

And than, run from command line:

```bash
php script.php command-name --email=me@example.com
```

### Log Messages

```php
Console::log('Plain Log'); // stdout
```

```php
Console::success('Green log message'); // stdout
```

```php
Console::info('Blue log message'); // stdout
```

```php
Console::warning('Yellow log message'); // stderr
```

```php
Console::error('Red log message'); // stderr
```

### Execute Commands

Function returns exit code (0 - OK, >0 - error) and writes stdout, stderr to reference variables. The timeout variable allows you to limit the number of seconds the command can run.



```php
$stdout = '';
$stderr = '';
$stdin = '';
$timeout = 3; // seconds
$code = Console::execute('>&1 echo "success"', $stdin, $stdout, $stderr, $timeout);

echo $code; // 0
echo $stdout; // 'success'
echo $stderr; // ''
```

```php
$stdout = '';
$stderr = '';
$stdin = '';
$timeout = 3; // seconds
$code = Console::execute('>&2 echo "error"', $stdin, $stdout, $stderr, $timeout);

echo $code; // 0
echo $stdout; // ''
echo $stderr; // 'error'
```

## System Requirements

Utopia Framework requires PHP 7.1 or later. We recommend using the latest PHP version whenever possible.

## Authors

**Eldad Fux**

+ [https://twitter.com/eldadfux](https://twitter.com/eldadfux)
+ [https://github.com/eldadfux](https://github.com/eldadfux)

## Copyright and license

The MIT License (MIT) [http://www.opensource.org/licenses/mit-license.php](http://www.opensource.org/licenses/mit-license.php)