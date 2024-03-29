---
notice: 'This file is imported and can be edited at https://github.com/amphp/cache/blob/2.x/README.md'
title: 'Cache Data in Concurrent PHP Applications'
description: 'Learn how to cache data to serve requests faster in a concurrency safe way.'
image: undraw/undraw_memory_storage.svg
permalink: /cache
source: 'https://github.com/amphp/cache/blob/2.x/README.md'
layout: docs
---
AMPHP is a collection of event-driven libraries for PHP designed with fibers and concurrency in mind.
`amphp/cache` specifically provides a cache interface and multiple implementations of it.

[![Latest Release](https://img.shields.io/github/release/amphp/cache.svg?style=flat-square)](https://github.com/amphp/cache/releases)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/amphp/cache/blob/master/LICENSE)

## Installation

This package can be installed as a [Composer](https://getcomposer.org/) dependency.

```bash
composer require amphp/cache
```

## Usage

### AtomicCache

### Cache

```php
<?php

namespace Amp\Cache;

interface Cache
{
    public function get(string $key): mixed;

    public function set(string $key, mixed $value, int $ttl = null): void;

    public function delete(string $key): ?bool;
}
```

### LocalCache

### NullCache

Cache implementation that just ignores all operations and always resolves to `null`.

### PrefixCache

### SerializedCache

### StringCache

### StringCacheAdapter
