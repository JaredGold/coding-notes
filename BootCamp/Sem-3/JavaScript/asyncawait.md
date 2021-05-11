# Async Await

Instead of promises we can use the terms async await

"An async function is a function declared with the **async** keyword. Async functions are instances of the AsyncFunction constructor, and the **await** keyword is permitted within them. The **async** and **await** keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains." - MDN

#### Async functions

Will always return a promise that either:

1. Resolves to the value explicitly returned from the function
2. Rejects with an error thrown from the function

```js
function promiseGreeter(name){
    return new Promise ((resolve, reject) => {
        if(!name){
            reject("Name cannot be null.");
        }
        resolve(`Hello ${name}`)
    })
}
```

```js
async function asyncGreeter(name){
    if(!name) {
        throw "Name cannot be null";
    }
    return `Hello ${name}`
}
```



**async** functions are used to enable the use of **await** not to avoid using promises

```js
async function processData(source){
    let data = await getDataAsync(source); // if this doesn't resolve, throws error
    return shapeData(data;)
}
```

* The **await** expression can only be used in an **async** function
* It causes **async** function execution to pause until a Promise is settles
* It forces synchronous code execution in the context of the **async** function

### Why use async/await

```js
function processData(source){
    getData(source)
        .then((response) => {
        	response.json().then((data) => {
                showData(data);
            })
    	})
}
```

```js
async function processData(source) {
    let response = await getData(source);
    let data = await response.json()
    showData(data)
}
```



# Error handling

In the error handling with this we want to use a `try/catch` block