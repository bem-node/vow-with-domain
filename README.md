<a href="http://promises-aplus.github.com/promises-spec"><img src="http://promises-aplus.github.com/promises-spec/assets/logo-small.png" align="right" /></a>
Vow [![Build Status](https://secure.travis-ci.org/dfilatov/jspromise.png)](http://travis-ci.org/dfilatov/jspromise)
=========

Promises/A+ implementation.
See https://github.com/promises-aplus/promises-spec.

Getting Started
---------------
###In the Node.js###
You can install using Node Package Manager (npm):

    npm install vow

###In the Browsers###
```html
<script type="text/javascript" src="vow.min.js"></script>
```
Also RequireJS module format supported.

API
---
####Vow.promise()####
Create promise
````javascript
var promise = Vow.promise();
````
###Promise API###
####fulfill(value)####
Fulfill promise with given ````value````
````javascript
var promise = Vow.promise();
promise.fulfill('completed'); // fulfill promise with 'completed' value
````
####reject(reason)####
Reject promise with given ````reason````
````javascript
var promise = Vow.promise();
promise.reject(Error('internal error')); // reject promise with Error object
````
####isFulfilled()####
Returns whether the promise is fulfilled
````javascript
var promise = Vow.promise();
promise.isFulfilled(); // returns false
promise.fulfill('completed');
promise.isFulfilled(); // returns true
````
####isRejected()####
Returns whether the promise is rejected
````javascript
var promise = Vow.promise();
promise.isRejected(); // returns false
promise.reject(Error('internal error'));
promise.isRejected(); // returns true
````
####isResolved()####
Returns whether the promise is fulfilled or rejected
````javascript
var promise = Vow.promise();
promise.isResolved(); // returns false
promise.fulfill('completed'); // or promise.reject(Error('internal error'));
promise.isResolved(); // returns true
````
####then([onFulfilled], [onRejected])####
Arranges for:
  * ````onFulfilled```` to be called with the value after promise is fulfilled,
  * ````onRejected```` to be called with the rejection reason after promise is rejected.
 
Returns a new promise. See [Promises/A+ specification](https://github.com/promises-aplus/promises-spec) for details.

````javascript
var promise = Vow.promise();
promise.then(
    function() { // to be called after promise is fulfilled
    },
    function() {// to be called after promise is rejected        
    });
````
####fail(onRejected)####
Arranges to call ````onRejected```` on the promise's rejection reason if it is rejected.
####spread([onFulfilled], [onRejected])####
Like "then", but "spreads" the array into a variadic value handler.
````javascript
promise.spread(onFulfilled, onRejected);
````

###Vow API###
####isPromise(value)####
Returns whether the given ````value```` is a promise.
````javascript
Vow.isPromise('value'); // returns false
Vow.isPromise(Vow.promise()); // returns true
````

####when(value, [onFulfilled], [onRejected])####
Static equivalent for promise.then. If given ````value```` is not a promise, ````value```` is equivalent to fulfilled promise.

####isFulfilled(value)####
Returns whether the given ````value```` is fulfilled. If ````value```` is not a promise, ````value```` is equivalent to fulfilled promise.

####isRejected(value)####
Returns whether the given ````value```` is rejected. If ````value```` is not a promise, ````value```` is equivalent to fulfilled promise.

####isResolved(value)####
Returns whether the given ````value```` is resolved (fulfilled or rejected). If ````value```` is not a promise, ````value```` is equivalent to fulfilled promise.

####fulfill(value)####
Returns a promise that has already been fulfilled with the given ````value````. If ````value```` is a promise, returned promise will be fulfilled with fulfill/rejection value of given promise.

####reject(reason)####
Returns a promise that has already been rejected with the given ````reason````. If ````reason```` is a promise, returned promise will be rejected with fulfill/rejection value of given promise.

####resolve(value)####
Returns a promise that has already been fulfilled with the given ````value````. If ````value```` is a promise, returns ````promise````.

####all(promises)####
Returns a promise to be fulfilled only after all the items in ````promises```` is fulfilled, or to be rejected when the first promise is rejected.

####allResolved(promises)####
Returns a promise to be fulfilled only after all the items in ````promises```` is resolved.

####any(promises)####
Returns a promise to be fulfilled only any item in ````promises```` is fulfilled, or to be rejected when the all items is rejected.

####timeout(promise, timeout)####
Returns a promise to be rejected after a ````timeout```` if ````promise```` does not resolved beforehand.
