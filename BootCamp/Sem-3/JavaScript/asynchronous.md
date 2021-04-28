# Asynchronous

By default javascript is synchronous code, also known as blocking code. This means that each statement of code can be run one at a time and then when finished it can move on to the next. Javascript can only use one thread at a time by default.

#### Problem

* It is a bad user experience if a user has to sit and wait for each thing to load in sequence
* The browser also wants to render things constantly (6ms). If we are blocking that then nothing can re-render and looks like the browser has frozen.

When a code is run Asynchronous the request of code is made but it is not worried about what happen next until the response is received.

#### Example

* `setTimeout` is async
* when the specified time has passed, the callback function is placed on the callback queue
* When the call stack is empty, the callback function is executed

```js
console.log(1);

setTimeout(() => {
    console.log(2);
}, 5000);

console.log(3);

//----- console
// 1
// 3
// (5 sec pause)
// 2
```

---

The way that multithreaded Async works is using the **call stack**, **callback queue**, and **event loop**

### Call Stack

* How JS keeps track of the execution order of it's code
* As the main thread runs, any function calls are pushed as **frames** (local execution contexts) on the stack
* Once the function has finished executing it pops off the top
* LIFO (Last In, First Out)

### Callback Queue

* How js processes responses from async functions
* when an async function completes its callback function is pushed onto the callback queue
* Callbacks in the callback queue are not placed on the call stack until it is completely empty
* FIFO (First In, First Out)

### Event Loop

the event loop handles async functions calls by:

* placing callback functions on the **callback queue** when they are ready to be executed
* placing callback functions from the queue onto the **call stack** when it is empty'



# `setTimeout(() => {}, 1000)`

Set timeout is how we make things not synchronous

