# Promises

A Promise is a place holder for a future event. Used in Async coding.

```js
myPromise = Promise.resolve("myPromise");
// which looks like bellow
```

```
Promise {<fulfilled>: "myPromise"}
    __proto__: Promise
    catch: ƒ catch()
    constructor: ƒ Promise()
    finally: ƒ finally()
    then: ƒ then()
    Symbol(Symbol.toStringTag): "Promise"
    __proto__: Object
    [[PromiseState]]: "fulfilled"
    [[PromiseResult]]: "myPromise"
```

* A JS Object
* Available methods: `.then`, `.catch`,`.finally`
* A status - or state - that is **immutable**
* A value that depends on the **status**

#### Note on `setTimeOut`

* Takes 2 params
* Callback function, added to the **call stack**
* Time to wait before executing that function in ms

```js
setTimeout(()=>{
    console.log("This waits 2 seconds")
}, 2000)
```

---

# Examples:

```js
let myFirstPromise = Promise.resolve("My first promise, yay")

myFirstPromise.then(/*accepts a function*/ function(value){
    console.log(value + '!!'); // My first promise, yay!!
})

myFirstPromise.then(value => console.log(value+'!!'))
```

```js
letMyFirstRejection = Promise.reject("Error Occured")
myFirstRejection.catch(reason => console.error(reason))
// you can not do then with a rejection
```

#### Better Ex

```js
function squareNumber(number){
    return new Promise((resolve, reject) => {
        if(typeof number !== 'number'){
            reject(new Error("Input must be a number"))
        }
        resolve(number * number)
    })
}

squareNumber(5).then(squaredNumber => console.log(squaredNumber)); //25
squareNumber("5").catch(error => console.log(error.message)); // "Input must be a number"

// the correct way to handle it is stringing them all together as bellow
squareNumber("5")
    .then(squaredNumber => console.log(`The squared number is ${squaredNumber}`))
    .catch(error => console.error(error.message))
    .finally(() => console.log("The promise has finished"))
```

#### NOT BLOCKED?

That's right this code is not blocked and is running asynchronously

```js
function squareNumber(number){
    return new Promise((resolve, reject) => {
        if(typeof number !== 'number'){
            reject(new Error("Input must be a number"))
        }
        resolve(number * number)
    })
}

squareNumber("5")
    .then(squaredNumber => console.log(`The squared number is ${squaredNumber}`))
    .catch(error => console.error(error.message))
    .finally(() => console.log("The promise has finished"))

console.log("I am meant to be last")

// ---- output ---- //
// I am meant to be last
// Input must be a number
// The promise has finished
```

---

# Then

*onResolve*

- Takes a callback function
- **Always** returns a promise
- Can be chained forever

# Catch

*onReject*

- Takes a callback function
- Will handle any **rejected promise** in the chain
- Will also handle any **thrown error** in the chain



ex:

```js
function generateRandomNumber(limit){
    console.log("Generating number between 1-"+limit);
    return new Promise((resolve, reject) => {
        setTimeout(()=>{
            if(typeof limit !== 'numbeer'){
                reject(new Error("Input must be a number"));
            }
            const randomNumber = Math.ceil(Math.random() * limit)
            resolve(randomNumber)
        }, 1000)
    })
}

generateRandomNumber(10)
	.then(number => console.log("The number is "+number))
    .catch(error => console.error("Caught Error: " + error.message))
```

You can also daisy chain the then blocks passing the value down in a return statement. For example below we run the code then pass the answer to the first then block, after it runs it passes it's return to the next block and finally one more time on the final block. The below code results a little strange but - 
Generating number between 1-10
The number is 3
Double the number is 6
The answer is 42

This gets 42 because the final then block returns 42

```js
function generateRandomNumber(limit){
    console.log("Generating number between 1-"+limit);
    return new Promise((resolve, reject) => {
        setTimeout(()=>{
            if(typeof limit !== 'numbeer'){
                reject(new Error("Input must be a number"));
            }
            const randomNumber = Math.ceil(Math.random() * limit)
            resolve(randomNumber)
        }, 1000)
    })
}

generateRandomNumber(10)
	.then(number => {
    	console.log("The number is " + number)
    	return number;
	})
	.then(number => {
    	console.log("Double the number is " + number * 2);
    	return 42
	})
	.then(answer => console.log("The answer is " + answer))
	})
    .catch(error => console.error("Caught Error: " + error.message))

```

We can abstract it further if there is more we want from our code block as below:

```js
function generateRandomNumber(limit){
    console.log("Generating number between 1-"+limit);
    return new Promise((resolve, reject) => {
        setTimeout(()=>{
            if(typeof limit !== 'numbeer'){
                reject(new Error("Input must be a number"));
            }
            const randomNumber = Math.ceil(Math.random() * limit)
            resolve(randomNumber)
        }, 1000)
    })
}

function doubleNumber(num){
    return new Promise((resolve, reject) => {
        if (num < 0) {
            reject(new Error("Can't double negative number"))
        }
        resolve(num * 2)
    })
}

function logIfSmall(num){
    if (num > 15){
        throw new Error("That number is too big")
    } else{
        console.log("The doubled number is " + num)
    }
}

generateRandomNumber(10)
	.then(number => {
    	console.log("The number is " + number)
    	return number;
	})
	.then(doubleNumber)
    //.then(double => console.log("The number doubled is: " + double))
	.then(logIfSmall)
    .catch(error => console.error("Caught Error: " + error.message))
```

---

# Refactoring 'Callback Hell'

*http://callbackhell.com/*

Callback hell is a super difficult code with a bunch of nested callbacks

* Nested functions rely on prior function being finished
* Pyramid of DOOOOOM

Accessing an API will look like this

```js
document.getElementByID("btn").addEventListener('click', ()=>{
    // $ is a jquery request
    $.getJSON("https://icanhazdadjoke.com/", (response) => {
        console.log("Got Joke: " + response.joke)
    })
})
```

If we wanted to log all of the jokes we would have to have a pause as each joke would be pulled in different speeds and logging them would mean a lot of the jokes would not come through. The below is a very bad example that works. (THIS IS AN EXAMPLE OF CALLBACK HELL)

```js
document.getElementByID("btn").addEventListener('click', ()=>{
    let jokes = []
    $.getJSON("https://icanhazdadjoke.com/", (response) => {
        jokes.push(response.joke)
        $.getJSON("https://icanhazdadJoke.com/", (response) => {
            jokes.push(response.joke)
            $.getJSON("https://icanhazdadJoke.com/", (response) => {
            	jokes.push(response.joke)
                $.getJSON("https://icanhazdadJoke.com/", (response) => {
            		jokes.push(response.joke)
                    $.getJSON("https://icanhazdadJoke.com/", (response) => {
            			jokes.push(response.joke)
                        console.log(jokes)
        			})
        		})
        	})
        })
    })
})
```

The way we can fix this is as below with promises. Still not absolutely clean. Also not asynchronous

```js
function getJoke() {
    return new Promise((resolve, reject) =>{
         $.getJSON("https://icanhazdadjoke.com/", (response) => {
             if (response){
                 resolve(response.joke)
             }
             reject(new Error("Failed to get Joke"))
         }
    })
}

document.getElementByID("btn").addEventListener('click', ()=>{
        let jokes = []
    	getJoke()
            .then(joke => {
            	jokes.push(joke)
            	return getJoke()
       		 })
        	.then(joke => {
            	jokes.push(joke)
            	return getJoke()
       		 })
        	.then(joke => {
            	jokes.push(joke)
            	return getJoke()
       		 })
        	.then(joke => {
            	jokes.push(joke)
            	return getJoke()
       		 })
        	.then(joke => {
            	jokes.push(joke)
            	console.log(jokes)
       		 })
            .catch(error => console.error(error.message);
    }
```

The below is the final fixed version. 

```js
function getJoke() {
    return new Promise((resolve, reject) =>{
         $.getJSON("https://icanhazdadjoke.com/", (response) => {
             if (response){
                 resolve(response.joke)
             }
             reject(new Error("Failed to get Joke"))
         }
    })
}

document.getElementByID("btn").addEventListener('click', ()=>{
        let promiseArray = [];
        for (let i=0; i < 5; i++){
            promiseArray.push(getJoke())
        }
        	Promise.all(promiseArray)
                .then(jokeArray => console.log(jokeArray))
            	.catch(error => console.error(error.message);
    }
```

**<u>Promise.all() will reject if there are any fail or rejects</u>**

