# Variables

#### What is a variable?

* A variable is a container that stores a value. 
* It can be updated and used(called) multiple times.
* They're named, meaning it is easy to refer to them
* They help us reuse code
* If you want to change something you only have to change it in one place.
* <u>**USE MEANINGFUL NAMES**</u>

**D**ont **R**epeat **Y**ourself (DRY) is a commonlly used term to remind you to make and use variables.

#### Syntax

* Variables are written in `snake_case`
* They are assigned using the `=` operator

```ruby
first_name = "John"
last_name = "Smith"
age = "32"
```

#### Changing the value of a variable

If you have created a variable and wish to change the value of the variable you can do so like below

```ruby
age = 20
age + 5								# This would return 25 althought age still euquals 20
age = age + 5					# age now equals 25
age += 5							# age now equals 30
age -= 5							# age now equqls 25
```



### Constants

Constant is a container that ***shouldn't*** change while the program is running (but in Ruby, they can)
* Starts with a capital letter
* Underscores serpate multiple words
* Often all caps

```ruby
tax = 0.1 					# Plain variable
VALUE_OF_PI = 3.14	# Constants
```



