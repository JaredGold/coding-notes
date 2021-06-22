# Intro

#### `'use strict';`

If you place `'use strict';` at the top of the script you force the entire file to be strict. This is best way to make secure code. Strict mode allows you to see visible errors when errors are created instead of them hiding. Strict mode also reserves words for variables if they will be used.



### Creating a function

You can create a function many ways in javascript. You can use function expressions or you can do function declaration.  A function declaration can be placed anywhere in the code and called at any moment where a function expression can only be called after it is first created in the code. A function expression forces cleaner code as you have to keep all of your functions at the top of the code.

```js
// function declaration
function calcAge (birthYear){
    return 2037 - birthYear;
};

// function expression
const calcAge = function (birthYear) {
    return 2037 - birthYear;
}

// Arrow functions
const calcAge = birthYear => 2037 - birthYear; 
```

