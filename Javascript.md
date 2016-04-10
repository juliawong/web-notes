# Javascript

## Promises

http://robotlolita.me/2015/11/15/how-do-promises-work.html
https://www.promisejs.org/
https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise

* Represents the result of a asynchronous computation
* Operation that hasn't completed yet, but is expected in the future
* e.g. waiting at a restaurant, a buzzer is like a promise for a future table, when it buzzes you get your table
* Define success and failure methods

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

### Syntax

`new Promise(function(resolve, reject) { ... });
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

``` JavaScript
p1.then(function(value) {
  // Success handler
}, function(reason) {
  // Error handler
});
```
