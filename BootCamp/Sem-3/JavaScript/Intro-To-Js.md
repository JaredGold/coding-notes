# Intro to Javascript

#### Variables

To declare a variable you can use `var`, `let` or `const`. 
`const` is a constant variable which can only be declared once.

```js
let test = 'test'
var num = 32
const isFun = true
```

#### String Interpolation

String interpolation can be done similarly to ruby but using `${something}`.
In order for it to be interpolated it must also be denoted using back ticks - \`

```js
let name = 'Jared'
console.log(`My name is ${name}`)
```

#### Hash

A hash is created the same way as ruby. A hashes key can be accessed differently though as seen below.

```js
var hash = {
	name: "jared",
    age: "26",
}

hash.name
```

#### Array

An array is created exactly as ruby

Same as always the blow are some methods you can run on arrays.

| code                           | what it does               |
| ------------------------------ | -------------------------- |
| `array.length;`                | Returns length of array    |
| `array.includes('something');` | Checks if item is in array |
| `array.push('something');`     | Adds items to the end      |
| `array.unshift('something');`  | Add items to the start     |
| `array.pop();`                 | Removes last element       |
| `array.shift()`                | Removes first element      |



You also have the ability to do something called `splice`. Splice allows you to remove items from an array at a specific spot.

`array.splice(1,3)` would splice the item in the array index of 1 and the next 3 items.

```js
var array = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

array.splice(1,3);	//removes 'orange', 'yellow', 'green'

array;				//returns ['red', 'blue', 'indigo', 'violet']
```



To combine arrays you can use the `array.concat(second_array)` which combines the two arrays.

```javascript
var colors = ['red', 'green', 'blue']
var hues = ['purple', 'orange', 'pink']

var combined_colors = colors.concat(hues)

combined_colors;		// ["red", "green", "blue", "purple", "orange", "pink"]
```



#### Output and Input

Javascript does not have input or output. The way we output is by using the `console` object. 

Inside your the browser console you can see some warnings and logs with the bellow.

```javascript
console.log("Hello World")					// log message
console.warn("This is a warning message")	// orange log message
console.error("This is an error message")	// red log message
```

To access pop up windows you can use the bellow

```javascript
alert("This is an alert")				//creates typical pop up
prompt("What is your name?")			//creates pop up with input section

let name = prompt("What is your name?")	//saves user input to variable
```



#### Blocks and Scoping

In javascript you can create blocks by using curly braces. Anything created in the curly brace by using `let` or `const` can only be used in the block. If you want a variable to save outside the scope you can use `var` although it is best practice not to.

```javascript
let x = "sarah";
{
  console.log(x);			// "sarah"
}

console.log(x);				// "sarah"

{
  let y = "mary";
  console.log(y);			// "mary"
}

console.log(y);				// y is undefined
```



#### Math methods

https://www.w3schools.com/js/js_math.asp



## Control Structures

Common control flow structures are

* `if`
* `if else`
* `if elseif`
* `while`
* `switch`
* `for`

These structures are the same as javascript and work the same way although it runs the block

```js
let coinFlip = 'Heads'

if (coinFlip == 'Heads'){
    console.log("The coin landed with heads facing up!")
} else {
    console.log("The coin landed with tails facing up!")
}
```

```javascript
let newPassword = 'Password123'

if (newPassword[0] != newPassword.toUpperCase()[0]){
    console.log("Password does not start with a capital letter!");
} else if (newPassword.toLowerCase().includes("password")){
    console.log("Password should not use easy-to-guess words!");
} else {
    console.log("Password is okay!");
}
```

Switch is much better when  it comes to speed and comparing to if statements

```javascript
let userFavoriteColor = "pink";

switch (userFavoriteColor){
    case "red":
        console.log("The user's favorite color is RED!");
        break;
    case "orange":
        console.log("The user's favorite color is ORANGE!");
        break;
    case "yellow":
        console.log("The user's favorite color is YELLOW!");
        break;
    default:
        console.log("The user's favorite color is not in the rainbow!");
        break;
}
```

###### Falsey Values

Falsey values in JavaScript as are below

* `false`
* `0`
* `""`
* `NaN`
* `null`
* `undefined`



## Loops

Loops are the same as Ruby but can be seen like below

#### For

For repeats a block of code

```javascript
for (let counter = 0; counter < 5; counter++){
    console.log(`This message has appeared ${counter} previous times.`)
}
```

or

```js
var storedPassword = "password123";

for (let attemptsRemaining = 5; attemptsRemaining > 0;){
    let userInput = prompt("What is the password?");
    if(userInput == storedPassword) {
        break;
    } else {
        attemptsRemaining--;
    }
}
```

#### While

While repeats while true

```js
let olympicMedals = 0;

while (olympicMedals < 10){
    olympicMedals++;
    console.log("You won another Olympic medal!");
}
console.log("Okay, you have 10, that's enough for one day!");
```



### Looping of an Array

#### `forEach`

forEach will loop over every item in the array

```js
let rainbow = ['r', 'o', 'y', 'g', 'b', 'i', 'v'];

rainbow.forEach(color =>{
    console.log(`This fancy color ${color} is in the rainbow!`)
})
```



#### `map`

Map does the same as for each but saves in a new array

```js
let rainbow = ['r', 'o', 'y', 'g', 'b', 'i', 'v'];

let capitalRainbow = rainbow.map(color => {
    return color.toUpperCase();
})
```



#### `do...while`

A do...while loop will run the doo first then check the while second.

```javascript
do {
    something
} while (condition == true)
```



#### `for`

A for loop runs code a pre determined amount of times

```javascript
for (initialization; condition; final-expression) {
     code here
 }
```

example:

```javascript
for (let i=0; i<10; i++) {
    console.log(`i: ${i}`)
} 
console.log("Our loop is finished")
```

#### `for of` and `for in`

When wanting to iterate over an array or object (hash) we can use a `for`  loops. Similar to `for each do |x|` in ruby.

```javascript
// an array
for (let element of array) {
    code
}

// an object
for (let key in object) {
    code
}
```

example:

```javascript
let pets = ["cat", "dog", "fish"]

for (let pet of array) {
    console.log(`I have a ${pet}`)
}

/*      ouputs ----
        I have a cat
        I have a dog
        I have a fish				*/

let person = {
    name: "John",
    hairColour: "brown",
    eyeColour: "green"
}

for (let key in person) {
    console.log(`My ${key} is ${person[key]}`)
}
/*		outputs ----
		My name is John
		My hairColour is brown
		My eyeColour is green			*/
```

example:

```javascript
function loopOverArray(directions){
    let obj = {}
    for (let item of directions){
        if (obj[item] >= 0){
            obj[item]++;
        } else {
            obj[item] = 1;
        }
    }
    return obj
}

function loopOverObject(object){
    let array = []
    for (let key in object){
        console.log(`Key: ${key}; Value: ${object[key]}`);
    }
}

function findUser(users, usr, pwd){
    for (let user of users){
        if (user.username == usr && user.password == pwd){
            return user
        }
    }
    return false
}
```



#### `break` and `continue`

When you want to break out of an iterated loop you can use break

```js
while (true) {
    console.log("Before the break")
    break
    console.log("This code won't execute")
}

console.log("After the loop")
```

```js
let i = 0
while (i < 10) {
    if (i === 7) {
        console.log("Lucky number 7 boi")
        console.log("Before the continue")
        continue
    }
    console.log(`i: ${i}`) // This code is unreachable when i === 7 as the continue skips it
}
```



## Functions

There are multiple forms of functions although some more straight forward than others. The first form of a function is the simple `function()`

#### `function()`

The function requires `()` to be run.

```js
function(item){
    // do something here
	return newItem
}
```



#### Arrow Function

An arrow function is similar to a regular function but uses less memory when defined

```js
// Traditionally declared function
function addTwo(num1, num2) {
    return num1 + num2
}

// First step is removing the keyword 'function' and place arrow between 
// the argument and opening body bracket. We save this to the reference 'addTwo'
const addTwo = (num1, num2) => {
    return num1 + num2
}

// Next is removing the brackets and the keyword `return` -- the return is implied
const addTwo = (num1, num2) => num1 + num2
```

 There are some important differences depending on the amount of arguments and lines of code in the function. For example:

```js
// If the function only takes one argument, we can omit the parentheses around the argument.
const takesOneArgument = arg => arg * 2

// When a function performs multiple lines of code, the curly braces are required and the 
// `return` keyword needs to be explicity called if required
const doesManyThings = arg => {
    if(arg < 0) {
        throw "doesManyThings does not accept your negative input"
    }
    return arg * 2
}
```

