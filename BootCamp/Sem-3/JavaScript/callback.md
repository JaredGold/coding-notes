# Callback function

A callback function is the ability to call a function in a function. You can create one like below.

```js
function processInput (input, callback){
    callback(input);
}

function greet(name){
    console.log(`Hello ${name}`)
}

function excitedGreet(name){
    console.log("HI THERE " + name.toUpperCase() + "!!!!!!!" )
}

processInput("Jared", greet);	// note greet does not look like `greet()`
processInput("Kim", excitedGreet);
```

This allows us to create modular and reusable code

Below is another example

```js
// Math functions
function add(a,b){
    console.log(a+b)
}

function multiple(x,y){
    console.log(x*y)
}

function doMath(num1, num2, cb){
    console.log("processing");
    cb(num1, num2)
}

doMath(2,5, (a,b) =>{
    console.log( a ** b)
})

doMath(10,5, add);
doMath(12,13, multiply)
```



```js
function modifySentence(sentence, modifier) {
    return sentence.split(" ").map(modifier).join;
}

function capitalise(word) {
    return word[0].toUpperCase() + word.substring(1);
}

function noCovid(word){
    return word.toLowerCase() === 'covid19' ? '####' : word
}

console.log(modifySentence("hello there friend", capitalise));
// Hello There Friend

console.log(modifySentence("COVID19 is a big problem", noCovid));
// #### is a big problem
```



---

You can also do the same thing using the `forEach` loop

```js
const people = ["Jared", "Kim", "Teddy", "Ezra"]

people.forEach(function (person)){
	console.log(person);
}

people.forEach(person => {
    console.log(person)
})

// the above does the same as the below

function logger(element){
    console.log(element);
}

people.forEach(logger);

// the below uses index.

people.forEach((person,index) => console.log(`${index + 1}. ${person}`));
```



#### `Array.map()`

The array map creates a new array instead of modifying the old array

```js
const numbers = [1,2,3,4,5];

console.log(numbers.map(number => number + 1)); // this is a callback

console.log(numbers.map(function(number){
    return number + 1;
}));

// cleaner below

function addOne(number) {
    return number + 1;
}
const double = (num) => num * 2;

console.log(numbers.map(addOne))
console.log(numbers.map(double))
```



#### `Array.filter()`

Array filter checks an array and as long as the object passes the given  rule it will create a new array with that in it.

```js
const people = ["Jared", "Kim", "Theodore", "Ezra"]

console.log(people.filter(name => name.length < 5)); // Kim , Ezra

// ---------------------------- //

function lessThanFive(word){
    return word.length < 5
}

console.log(people.filter(lessThanFive(name)))
```



---

## Callback Error Handling

*Error First Callbacks*

Error first callbacks is passing an error as the first line in the code so that if there are any errors it will run the error before anything else.

##### errorHandling.js	

```js
function doMath(num1, num2, callback){
    if (typeof num1 !== 'number' || typeof num2 !== 'number'){
        const err = new Error("Can only perform math on numbers")
        return callback(err); // it assumes the other (num1, num2) are not there
    }
    callback(null, num1,num2);
}

function multiply(err,a,b){
    if(err){return console.error(err.message)}
    console.log(a*b);
}

function add(err,x,y){
    if(err){return console.error(err.message)}
    console.log(x+y);
}


// doMath(2,5,multiply);
// doMath(3,3,add);
```

```js
function userName(name, callback){
    if (typeof name != 'string'){
        const error = new Error("Name must be a string");
        callback(error);
    } else if (name.length < 1){
        const error = new Error("Name can not be empty");
        callback(error)
    } else {
        callback(null, name)
    }
}

function greet(error, name){
    if (error){
        console.log(error.message);
        return
    }
    console.log (`hello ${name}`)
}
```

