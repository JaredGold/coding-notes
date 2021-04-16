# Exception Handling

Exception handling in ruby is where we have the `begin`, `rescue`, `end`

Exception handling in Javascript is very similar

We use the error handing of node.

#### `throw`

In javascript we use the term `throw` to say there is an error. It looks like below

`throw "this is an error"`

#### `try` and `catch`

If your code can run into an error and you need exception handing you wrap it in a `try` `catch` block.

```js
try {
    throw "This is an error"
} catch (e) {
    console.log(`Error: ${e}`)
} finally {
    console.log('finally!')
}
```

The try section will run any code and if at any time there is an error then catch will take over. No matter the situation it will always run the `finally` block.

Below is an example.

```js
const subtract = function (num1, num2) {
    let answer;
    
    try {
        answer = num1 - num2;
        if (isNaN(answer)){
            throw "Invalid input";
        }
        return answer;
    } catch (e) {
        console.log(`Error: ${e}`);
    }
}
```









---

## Error Types and Custom Errors

We've seen some basic error handling, lets now have a look at some common JavaScript Error types.

**ReferenceError**

Pretty simple, you've tried to access a variable that isn't in scope or hasn't been defined yet.

```js
function willThrow() {
    return foo // throws ReferenceError because foo hasn't been declared yet 
}
```

**SyntaxError**

Happens when the code you have written breaks JavaScript rules. For example function signatures that do not have brackets, arrays without comma separated values etc. These errors can't be handled except writing syntactically correct code.

```js
function willThrow(( {  // throws SyntaxError 
    return
}

5.toPrecision(2) //throws SyntaxError
```





**TypeError**

These errors occur most often when we call a function that isn't defined for that object type.

```js
let string = 'foo'
let number = 5

number.toPrecision(2)
string.toPrecision(2) // throws TypeError. No 'toPrecision' function on a string
```



## Custom errors

There's a lot of different error types out there but sometimes we'll want to create our own custom errors. We do this by extending the built-in Error class. We can overwrite the existing attributes (in this case `name`) and we can create our own attributes that don't exist in the base class (in this case `solution`) as well as creating custom functions.

```js
class ValidationError extends Error {
    constructor(message, solution) {
        super(message)
        this.name = "ValidationError"
        this.solution = solution
    }
}

function validateUser(userObject) {
    if (!userObject) {
        throw new ValidationError("No user exists", "Create an account before moving on")
    } else if (!user.name) {
        throw new ValidationError(
            "Missing field: name", 
            "You can add your name in the 'about me' section"  
1        )
    } else if (!user.email) {
        throw new ValidationError(
            "Missing field: email", 
            "Update your email in the preferences section"
        )
    }
    return userObject
}

try {
    validateUser(databaseData)
} catch (err) {
    alert("Something is missing! \n" + err.message + "\n" + error.solution)
}
```





Get used to writing error handling, especially when receiving input from users or from an API. You can never assume that data coming from an external source will be available exactly the way you expect it, and good programming takes that into account and handles potential problems gracefully.