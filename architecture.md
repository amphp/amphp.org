---
title: Architecture
description: Learn how to manage multiple coroutines, coordinate between them, and how to cancel pending operations.
image: undraw/undraw_city_life.svg
permalink: /architecture
layout: docs
---
Traditionally, PHP follows a sequential execution model.
The PHP engine executes one line after the other in sequential order.
Often, however, programs consist of multiple independent sub-programs with can be executed concurrently.

There have been various techniques for implementing concurrency in PHP over the years, e.g. callbacks and generators shipped in PHP 5.
These approaches suffered from the ["What color is your function"](https://journal.stuffwithstuff.com/2015/02/01/what-color-is-your-function/) problem, which we solved by shipping Fibers with PHP 8.1.
They allow for concurrency with multiple independent call stacks.

Fibers are cooperatively scheduled by the [event-loop](https://revolt.run), which is why they're also called coroutines.
It's important to understand that only one coroutine is running at any given time, all other coroutines are suspended in the meantime.

You can compare coroutines to a computer running multiple programs using a single CPU core.
Each program gets a timeslot to execute.
Coroutines, however, are not preemptive.
They don't get their fixed timeslot.
They have to voluntarily give up control to the event loop.

Any blocking I/O function blocks the entire process while waiting for I/O.
You'll want to avoid them.
If you haven't read the installation guide, have a look at the [Hello World example](/installation#hello-world) that demonstrates the effect of blocking functions.
The libraries provided by AMPHP avoid blocking for I/O.

## Coroutines

Coroutines are the basic concurrency primitive.
They can be created using `Amp\async()` returning a placeholder for the eventual result of the coroutine, a `Future`.
The result can be awaited and unwrapped by calling its `await()` method.
The passed closures are executed concurrently regardless of whether the returned futures are awaited or not, but we need to ensure we keep the process running until both operations are complete.

```php
<?php

$future1 = Amp\async(static function () {
    for ($i = 0; $i < 5; $i++) {
        echo '.';
        Amp\delay(1);
    }
});

$future2 = Amp\async(static function () {
    for ($i = 0; $i < 5; $i++) {
        echo '_';
        Amp\delay(0.5);
    }
});

$future1->await();
$future2->await();
```

## Future Combinators

Instead of awaiting each future sequentially, so-called combinators can be used.

{% include stub.md %}

## Running to Completion

Sometimes an application doesn't want to keep track of all pending operations.
Instead of awaiting specific operations, `Revolt\EventLoop::run()` can be used to run the event loop until it's done.

```php
Revolt\EventLoop::run();
```

## Cancellations

{% include stub.md %}