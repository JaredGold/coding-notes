# Data Types

## What are data types

#### Numbers

- Integer (Whole Numbers) `2`
- Floats (Decimal Points) `2.1471`

#### Strings

* Strings are just text (Note strings can have numbers in them but computers see them as text)

  `"Hello World! 127"`

#### Boolean

* Booleans can be true or false.

  `yellow = true`

  `isFalling = false`

#### Arrays

* Arrays are lists of items.

  `[1, 2.5, "green"]`

  *The above is an array with a mix of int's floats and strings*

* To go more into detail - Arrays can also be multiple dimensions

* A 2D array looks like this `[ [0 ,1 ,2] , [3, 4, 5] ]`

#### Hashes

* Hashes contains a list of Key Value Pairs (Can also just be seen as a list of data)

  ```ruby
  {
    "Sydney" => 2000,
    "Melbourne" => 3000,
    "Brisbane" => 4000
   }
  ```

#### Symbols

- TBD

  `:goodbye`



#### If you don't know what the class of a data type is:

The method `.class` can show us what class we are using.

```ruby
"Hello there".class # string
3.class							# int
12.247.class				# float
```



## Basic Arguments

##### Arithmetic Operators

| Type                    | Code |
| ----------------------- | ---- |
| Addition                | `+`  |
| Subtraction             | `-`  |
| Multiplication          | `*`  |
| Division                | `/`  |
| Modulus                 | `%`  |
| Exponent (To the Power) | `**` |

#### Maths

If you do any maths from an integer to an integer you get an integer back - `1 + 1 = 2`

If you do any maths from  an integer to a float you receive a float back - `1 + 1.0 = 2.0`

When you divide an int to an int you do not get to see a remainder. `10 / 3 = 3`

There are still **<u>Operator Precendence</u>** ~ Make sure to use () ~

1. `*` `/` `%` `**`
2. `+` `-`



### Strings

Strings are a sequence of characters that are surrounded by quote marks. Either double or single quotes will work with.

You can add 2 strings together using string concatenations

```ruby
"Hello" + "World"
"HelloWorld"
```



### Booleans

Booleans can hold only 2 values `true` or `false`

Booleans are written as below

```ruby
flight = true
fall = false
true
false
if x == true
```

Items can also hold the value of `nil` i.e. it returns with no value.

```ruby
x = nil
x = 1 + 2
x = 3

y = nil
y = "Hello " + "Word"
y = "Hello World"
```



## Type Coercion

Type coercion is when you want to change one data from one type to another. For example changing something from an integer to a string or float

```ruby
137.to_s 	# returns "137"
12.5.to_i # return 12
8.to_f 		# returns 8.0
```

You would use this if you try to change a string to a float to do an arithmetic equasion. Bellow is an example of a user input math command.

``` ruby
puts "First Number: "
x = gets.chomp						# Gets a string and chomps the return
puts "Second Number: "
y = gets.chomp
# We now have 2 strings but when you add strings together you would see "xy"
# To fix the above we need to change it
puts x.to_i + y.to_i
```





