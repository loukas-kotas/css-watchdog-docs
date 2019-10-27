
# Library 
Library includes all the functionality with the api in form of functions.

## Usage

In order to use the watchdog library, a new class instance should be created.
After that, you can call every available function.

* Note #1

Every function returns a promise. So you need to handle each function call as a promise.
Tip: use async/wait instead of catch/then in every function call.


#### Example

```
    const Watchdog = require('css-watchdog');
    ...
    const watchdog = new Watchdog(); 
    const font-size = watchdog.get_attribute_of_element('https://loukaskotas.com', 'about', 'font-size');

```

## Lifecycle Hooks

There are two lifecycle hooks:
1. beforeAll  --> Before every function call is executed
2. beforeEach --> Before each function call is executes

### beforeAll

It executes once with the Watchdog instance creation.
You need to provide it in the constructor while creating a class instance.

### beforeEach

It executes every time before a function call.
You need to provide it in the constructor while creating a class instance.

#### Example
```

const beforeEach = function() {
    console.log('I will execute')
}