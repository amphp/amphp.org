---
notice: 'This file is imported and can be edited at https://github.com/amphp/redis/blob/2.x/README.md'
title: 'Communicate with Redis Servers'
description: 'Learn how to efficiently communicate with Redis servers, enabling scalable and responsive data storage and retrieval.'
image: undraw/undraw_searching.svg
permalink: /redis
source: 'https://github.com/amphp/redis/blob/2.x/README.md'
layout: docs
---
AMPHP is a collection of event-driven libraries for PHP designed with fibers and concurrency in mind.
This package provides non-blocking access to [Redis](http://redis.io) instances.
All I/O operations are handled by [Revolt](https://revolt.run) event loop, so you should be familiar with the basics of it.

## Installation

This package can be installed as a [Composer](https://getcomposer.org/) dependency.

```bash
composer require amphp/redis
```

## Usage

```php
<?php

require __DIR__ . '/vendor/autoload.php';

use function Amp\Redis\createRedisClient;

$redis = createRedisClient('redis://');

$redis->set('foo', '21');
$result = $redis->increment('foo', 21);

\var_dump($result); // int(42)
```

## Security

If you discover any security related issues, please use the private security issue reporter instead of using the public
issue tracker.

## License

The MIT License (MIT). Please see [`LICENSE`](./LICENSE) for more information.
