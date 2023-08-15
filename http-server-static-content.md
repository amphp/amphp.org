---
notice: 'This file is imported and can be edited at https://github.com/amphp/http-server-static-content/blob/2.x/README.md'
title: 'Static File Serving'
description: "Learn how to serve static files with Amp's HTTP server."
image: undraw/undraw_logistics.svg
permalink: /http-server-static-content
source: 'https://github.com/amphp/http-server-static-content/blob/2.x/README.md'
layout: docs
---
This package provides a static content `RequestHandler` implementations for the [AMPHP HTTP server](https://github.com/amphp/http-server).

## Usage

**`DocumentRoot`** and **`StaticResource`** implement `RequestHandler`.

## Example

```php
<?php

use Amp\Http\Server\DefaultErrorHandler;
use Amp\Http\Server\RequestHandler\ClosureRequestHandler;
use Amp\Http\Server\Response;
use Amp\Http\Server\SocketHttpServer;
use Amp\Http\Server\StaticContent\DocumentRoot;
use Amp\Http\Status;

$router = new Amp\Http\Server\Router;
$router->setFallback(new DocumentRoot(__DIR__ . '/public'));
$router->addRoute('GET', '/', new ClosureRequestHandler(function () {
    return new Response(Status::OK, ['content-type' => 'text/plain'], 'Hello, world!');
}));


$server->start($router, new DefaultErrorHandler());
```