# Javascript

## Promises

* http://robotlolita.me/2015/11/15/how-do-promises-work.html
* https://www.promisejs.org/
* https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise
* https://egghead.io/series/js-console-for-power-users


* Represents the result of a asynchronous computation
* Operation that hasn't completed yet, but is expected in the future
* e.g. waiting at a restaurant, a buzzer is like a promise for a future table, when it buzzes you get your table
* Placeholder for values that will eventually be computed
* Define success and failure methods
* Plug value into an expression, delay execution of expression until needed

Don't use promises for:
* Notifying progress of computation, use Events
* Producing multiple values over time, use Streams or Observables
* Representing action, can't execute promises in order, use CPS

### States
Once a primise is fulfilled or rejected, it is immutable
The above is also known as settled
* Pending - initial, yet to be executed
* Fulfilled - successful competion of operation
* Rejected - failed operation

### Chaining
* Can transform the promise via another operation
* Use `.then` when doing something with the result
* Use `.done` when not doing anything with the result

### ECMAScript 2015 Syntax

`new Promise(function(resolve, reject) { ... });`
* Functions to fulfil and reject the promise, called upon completion of operation
`Promise.all(iterable);`
* Returns a promise that resolves when all promises in iterable have been settled
* Fail-fast
* If any reject, promise rejects with value of first rejected promise, discards all other promises

``` JavaScript
Promise.all([arr, of, vals]).then(function(value) { 
  console.log(value); // success 
}, function(reason) {
  console.log(reason); // failure
});
```

`Promise.race(iterable);`
* Returns a promise that is settled as soon as any of the promises in the iterable settles
* i.e. first come, first served
* Returns value or reason from first settled promise

``` JavaScript
Promise.race([arr, of, vals]).then(function(value) { 
  console.log(value); // success 
}, function(reason) {
  console.log(reason); // failure
});
```

`Promise.reject(reason)`
* Returns a promise object that is rejected with provided reason

``` JavaScript
Promise.reject(new Error("fail")).then(function(error) {
  // not called
}, function(error) {
  console.log(error); // failure
});
```

`Promise.resolve(value)`
`Promise.resolve(promise)`
`Promise.resolve(thenable)`
* Returns a promise ovject that is resolved with
  * Value - returned
  * Promise - resolves given promise
  * Thenable - returned promise follows that thenable

``` JavaScript
Promise.resolve("Success").then(function(value) {
  console.log(value); // "Success"
}, function(value) {
  // not called
});

var original = Promise.resolve(true);
var cast = Promise.resolve(original);
cast.then(function(v) {
  console.log(v); // true
});

var thenable = { then: function(resolve) {
  throw new TypeError("Throwing");
  resolve("Resolving");
}};
var p2 = Promise.resolve(thenable);
p2.then(function(v) {
  // not called
}, function(e) {
  console.log(e); // TypeError: Throwing
});
```

```
p.catch(onRejected);

p.catch(function(reason) {
   // rejection
});
```
* Returns a promise and deals with rejected cases
* Function takes rejection reason as arg

``` JavaScript
p1.then(function(value) {
  console.log(value); // "Success!"
  throw 'oh, no!';
}).catch(function(e) {
  console.log(e); // "oh, no!"
}).then(function(){
  // success
}, function () {
  // failure, not fired due to catch
});

```

```
p.then(onFulfilled, onRejected);

p.then(function(value) {
   // fulfillment
  }, function(reason) {
  // rejection
});
```
* Returns a promise with a callback for success and failure
* Each takes an arg, value or reason
* Chainable
* Automatically lifts regular values to a promise
* Disallows nested promises
* Exceptions are caught and reified as a rejected promise
* Invokes dependencies asynchronously

``` JavaScript
p1.then(function(value) {
  // Success handler
}, function(reason) {
  // Error handler
});
```

## Logging

* `console.log` is the usual one we see
* Different levels of logging - `warn`, `error`, `info`, `debug`
* Can pass in multiple args
  * `console.log({foo: barObj, a: bObj})`
  * `console.log("Hello %x", "world")`
  * Style output `console.log("This is my %coutput!", "color: blue; font-size 3em;")`
* `console.group` ideal for nesting other statements under it
  * `console.groupEnd()` end the group
  * `console.groupCollapsed` collapse all statements and only log root
* `console.assert` if statement false, outputs error
  * Won't prevent other lines from being executed
* `console.count` logs message and number of occurrences
* `console.time` tracks time for given key until `console.timeEnd` with same key
* `console.table` pretty-print tabular data e.g. array of objects
  * Second arg is columns to show

