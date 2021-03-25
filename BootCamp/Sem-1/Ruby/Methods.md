# Methods

### What is a Method

* Methods are actions of programming
* Its a sequence of instructions grouped together to do a task
* the group of instructions is given a method definition  and is given a name called method name

```ruby
def tie_my_shoes
    puts "grab shoe laces"
    puts "twist and tie them around"
    puts "end"
end
```



### Why use a method?

* **DRY** == **D**o **N**ot **R**epeat **Y**ourself
* It's very key to use DRY
* Methods allow us to do this
* Define a group of instructions ONCE

## Method Call

* Methods are only executed when they are called / invoked
* The syntax for calling a method is the name of the method
* Methods can be called any number of times in a program

```ruby
tie_my_shoes
```

### Passing Arguments

* Methods can be customized by passing arguments to it
* These arguments are variables
* The number of arguments in the definition must match the arguments in the method call

```ruby
def cook (item, cooking_time)
    puts "Add #{rice} and cook for #{cooking_time}"
end

cook("rice", 15)
```



### Named Arguments with Default Values

* When defining a method a default value can be assigned to the arguments
* If no value is passed to a method call the default value is taken
* If a value is passed to a method call, the default value is overwritten with the passed value

```ruby
def greeting(name: "Programmer", language: "Ruby")
    puts "hello #{name}! We heard you love #{language}!"
end

greeting
#=>hello Programmer! We heard you love Ruby!
greeting(name: "bob", language: javascript)
#=>hello bob! We heard you love javascript!
```



### Implicit Return vs Explicit Return

* Explicit return: using `return` will stop the method from going any further and reverts back to the initial call to continue the program
* Implicit return: Methods in ruby returns the last line executed by default, if no return keyword is used

```ruby
# Explicit Return
def add(a,b)
    return a + b
    #anything beyond this return does not execute
end
puts add (1,2) #=> 3

#Implicit Return
def add(a,b)
    a + b
end
puts add (1,2) #=> 3
```



### Store return values from a method

* Methods always return a value when they are called
* The values returned can be assigned to a variable for further operation in the program

```ruby
def multiply(a,b)
    a*b
end
answer = multiply(3,2) #=> 6
result = multiply(answer, 10) #=> 60
```

