# Control Structures

### What is a Control Structure

Control structure is also known as control flow. Control flow is a way for our programs to run specific ways depending on **IF** specific conditions were satisfied or not.

## Syntax

In ruby the flow starts with an `if` followed by the condition. It is then followed by the case of it is not meeting the condition by using `else` and finally you `end`.

``` ruby
if condition
    # Something to execute
else
    # Execute this if the if statement is false
end

temperature = 10
if temperature > 15
    puts "It's Warm"
else
    puts "Brr..."
end
```



#### Ternary Operator

* A Ternary operator is a shorthand for if/else statements. 
* They work best when there is only one line of code to be executed in both `if` and `else` blocks. 
* Instead of if and else statements, ternary  operators involves `?` and `:`

``` ruby
condition ? #executes if condition is true : #executes if condiotion is valse

raining = true
puts raining ? "Carry an umbrella" : "Don't carry an umbrella"
```



#### Case Statement

* Case statements start with a keyword `case` followed by a `variable`
* Every condition that can be matched to that variable is `when` statement
* If nothing matches `else` case is executed
* Do **NOT** use case statement for simple logic like just true or false

```ruby
capacity = 21
case capacity
    when 0
    	puts "You ran out of gas."
    when 1..20
    	puts "The tanks is almost empty. Quickly, find a gas satation!"
    when 21..70
    	puts "You should be okay for now"
    when 71..100
    	puts "The tank is almost full"
else
   puts "Error! Capacity is invalid value is (#{capacity})"
end
```



#### Logical Operator

- Logical operators compare if multiple Boolean conditions are true or false
- Three types of Logical operators are 
  - `and (&&)` - bot sides must be true
  - `or (||)` - one side must evaluate to true
  - `not (!)` - returns the opposite value

```ruby
true && true 	=> true
true && false 	=> false
false && false 	=> false

true || true 	=> true
true || false	=> true
false || false 	=> false

!true			=> false
!false			=> true
```



#### Short Circuit Logic

* Short circuit logic is when we combine multiple conditions together
* Execution of the consecutive conditions depends on which logical operator is being used and the value of the first Boolean
  * EXAMPLE BELOW: Since the first condition fails (num > 0) in the `and` operation, the ruby interpreter will not evaluate the second condition as false as `&&` anything returns false.

```ruby
raining = true
carry_umbrella = true

if raining && carry_umbrella
    pyts "You'll be fine"
else
    puts "You're gonna get drenched"
end

num = -20

if num > 0 && num % 2 == 0
    puts "number is positive and even"
elsif num > 0 && num % 2 == 1
    puts "number is positive and odd"
else
    puts "negative number"
end
```



#### Ruby Truthy and Falsy Values

In ruby only "false" and "nil" are falsy value, everything else is true.

```ruby
!false	=> true
!nil	=> true
!1		=> false
!0		=> false
!-1		=> false
!'word'	=> false
!true	=> false
```



## Loops

### What is a loop?

A loop is a way of repeating a bunch of instructions based on a certain condition.

The reason loops are useful is, we can define a bunch of instructions once and execute them a number of times.



#### Types of loops

**While Loop**: Starts with keyword `while` followed by a condition, if condition is true, executes the code until you hit the keyword `end`. Requires an explicit iteration.

```ruby
iterations = 0

while iterations < 5
    iterations += 1
    puts iterations
end
```

**For Loop**: Similar to a while loop except for the key word `for` followed by a range of values. Do not have to explicitly iterate.

```ruby
for num in 1..5
    puts num
end
```



#### Break and Next

**Break**: the `break` keyword automatically exits the loop, no matter if the condition is still true or not

```ruby
iterations = 0
while true
    iterations += 1
    puts "Iteration #{iterations}"
    break
end
```

**Next**: the `next` keyword will not execute further lines of code within that iteration of the loop and proceeds to it's next iteration.

```ruby
iterations = 0
while true
    iterations += 1
    if iterations % 2 != 0
        next
    end
    puts "Iteration #{iterations}"
end
```

