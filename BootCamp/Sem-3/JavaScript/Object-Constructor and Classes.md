​	

# Object Constructors and Prototypes

An object constructor is a function that defines properties with the **this** keyword. It is analogous to the **initialize** method in Ruby.

**`this`** is a self-reference to the object instance.

You can use the `new` keyword to create objects with the consutructor

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.awesome = true;
    
    this.shout = function() {
        return `${name} IS ${AGE} YEARS OLD!!!!`
    }
}

let awesomeGuy = new Person("Jared", 27)
console.log(awesomeGuy.shout())
```



### Prototype Property

Can be used to add a default property after object creation.

```js
let student = new Person("Bo", 22);
Person.prototype.role = "student"
```

The `prototyue` is a template object that is shared between all instances of the same constructor - in this case, `Person`.

Similar to a supeerclass in Ruby, except this isnt inheritance.

We can also use this propotype to define member functions outside of the constructor. This is considered best-practice. To call the function instead of using `${age}` it is `${this.age}`

```js
function Hero(name, level) {
    this.name = name;
    this.level = level;
}
Hero.prototype.shout = function() {
    return `My name is ${this.name!}`
}
```

---

# Classes

Classes are ES6 only and are syntactic sugar for object prototypes

`constructor` is equivalent to `initialize` in Ruby.

`this` refers to the object itself and is equivalent to using `@` in ruby

```js
class Rectangle {
    constructor(width, height){
        this.width = width;
        this.height = height;
    }
    area() {
        return this.height * this.width
    }
}

let rect = newRectangle(10,5)
console.log(rect.area())
```



#### JavaScript is OO, but not class-based

From MDN docs...

"Javascript **classes**, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript's existing prototype-based inheritance. The clas ssyntax ***does not*** introduce new object-oriented inheritance to model in JavaScript"



### Static Properties

Static properties are accessed with the class name instead of an instance variable

Use them to define properties that are common for all instances of a class.

```js
class StockItem {
    static total_qty = 0;

	constructor(description, qty) {
        this.description = description
        this.qty = qty
        StockItem.total_qty += qty
    }
}

let warehouse = [
    new StockItem("CPU", 10),
    new StockItem("Motherboard", 5),
    new StockItem("Ram", 20)
]

console.log(`Total Stock ${StockItem.total_qty}`)
```



### Class Inheritance

We can use the `extends` keyword to inherit from another class.
We can use the `super` keyword to execute the superclass function.

```js
class Animal {
    constructor(name){
        this.name = name
    }
    speak() {
        return `My name is ${this.name}!`
    }
}
class Dog extends Animal {
    constructor(name, breed) {
        super(name)
        this.breed = breed
    }
    speak() {
        return `Woof ${super.speak()} I'm a ${this.breed}!`
    }
}

let animal = new Animal("Ted")
console.log(animal.speak()) // My name is Ted!
let dog = new Dog("Marshall", "Cavalier")
console.log(dog.speak()) // Woof My name is Marshall! I'm a Cavalier
```

#### `Object.assign`

Used to add or modify properties for an object instance.
This is a form of **composition** - we are combining the properties of several objects into on object.

```js
const student = {
    name: "John",
    course: "none"
};
const genTechStudent = {
    course: "GenTech",
    start: "October"
};
const caStudent = {
    languages: ["ruby", "javascript"],
    speak: () => {
        console.log("I can do it!");
    }
};

let john = Object.assign(student, genTechStudent, caStudent);
console.log(john);
/*
{
name: "John",
course: "FastTrack",
start: "October",
languages: ["ruby", "javascript"]
speak: function () { console.log("I can do it!") }
}
*/
john.speak();
```

### Mixins

Class inheritance only allows on level of extension - a class can extend only one superclass

Mixins provide a way to define additional functions that can be implemented by an object or class, and ar elike interfaces in traditional OOP languages

Mixins are similar to the Ruby concept of **modules**

#### Mixin with objects

Mixin is an object that provides additional functionality.

Use `Object.assign` to add the mixin function to an object instance

An object can use as many mixins as needed

```js
// the mixin
let calculate = {
    add(b){
        return this.value + b;
    },
    subtract(b) {
        return this.value - b;
    },
    multiply(b) {
        return this.value * b;
    },
    divide(b) {
        return this.value / b;
    }
}

// the object prototype
let Number = function(value) {
    this.value = value
}

let numberOfDays = newNumber(5);
numberOfDays = Object.assign(numberOfDays, calculate)
console.log(numberOfDays.add(5))
```

#### Mixin with class

Use `Object.assign` with the class prototype to add the functionality of the mixin to a class.

```js
// the mixin

const area = {
    setUnit(units) {
        this.units = units
    },
    getArea() {
        return this.length * this.width
    },
    areaToString() {
        return `${this.getArea()} ${this.units}`
    }
}

// the class
class Rectangle {
    constructor(length, width) {
        this.length = length;
        this.width = width;
    }
}

Object.assign(Rectangle.prototype, area);
let shape = new Rectangle(3,5);
shape.setUnits("cm");
console.log(shape.areaToString());
```

