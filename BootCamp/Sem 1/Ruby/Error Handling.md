# Error Handling

#### Errors are essential

* Errors represent issues - invalid data from the user, programmer error, cloud services being unavailable
* It's your job as a programmer to expect these issues, and know how to handle them

#### The problem of Optimistic Code

* Your code makes a lot of assumptions until you are trained to avoid it, including assumptions about: 
  * The format of input
  * The user's knowledge of your application
  * The way your application will be used
  * That the environment works as expected (network connection available, for example)

#### Why handle errors?

* Errors that are not dealt with become unexpected paths in your code
* Failing to handle errors at best annoys the user, but it can also make your app unusable and even insecure

#### Informing the user

* Every time an error occurs, we could tell the user - however, this would be a poor user experience
* When possible deal with the error internally: try again or recover in some way
* If you need to fail - fail fast

## Catching errors with rescue

#### Handling Errors in Ruby - `rescue`

* Errors are easy to handle in Ruby
* Use `rescue` in a begin/end block or at the end of a method
* Your code to handle errors is between `rescue` and `end`
* `rescue` with no arguments catches all exceptions that derive from `StandardError`

```ruby
begin
    # Code that could error
rescue
    puts "Error occured"
end
```



#### Handling different types of errors

* You can include multiple rescue clauses to catch different types of errors
* Order them from more to least specific because Ruby will stop at the first matching rescue

```ruby
begin
    # Code that could error
rescue SomeSpecificError
    puts "Some specific error occured"
rescue StandardError
    puts "Error occured"
end
```



#### Using exception information

If you refer to a variable for the exception, you can access information about it

```ruby
begin
    # Code that could error
rescue StandardError => e
    puts "Error occured: #{e.message}"
end
```


## Raising Errors

* Use raise to explicitly raise an exception
* By default raises a RuntimeError
* Can specify an exception type

```ruby
# Specify an exception type
def validate_name(name)
    name = name.strip # Trim whitespace
    raise ArgumentError, "Name must not be empty" if name.empty?
    name
end

validate_name ""
```

```
Traceback (most recent call last):
		1: from myapp.rb:11:in `<main>'
myapp.rb:6:in `validate_name' : Name must not be empty
(ArgumentError)
```

## Create custom errors

* Writing your own errors allows you to represent custom issues
* For example, you could validate some user input and raise a custom error if it is invalid
* Each specific problem in your app can have its own error, so you can deal with each in its own way
* Gems will often have their own error subclasses

#### Defining Errors

* Subclass StandardError
* Call `raise`, passing your error class and message
* We can now use the `validate_name` function, and rescue `InvalidNameError` type errors when they occur

```ruby
class InvalidNameError < StandardError
end

def validate_name(name)
    name = name.strip # Trim whitespace
    raise InvalidNameError
    	"Name must not be empty" if name.empty?
    name
end
```


## Retry, else and ensure

#### Retry

* Take an example of user input of two numbers to divide
* It would be nice to repeat things until an error is not raised
* We can achieve this with the `retry` keyword

```ruby
def divide (dividend, divisor)
    dividend/divisor
end

puts "--- Division App ---"

begin
    puts "Give me a number"
    number1 = gets.to_i
    puts "Give me another number"
    number2 = gets.to_i
    answer = dividde(number1,number2)
    puts answer
rescue StandardError => e
    puts "An error occured: #{e.inspect}"
    retry
end
```

#### Else and Ensure

* `else` after last rescue block and before `end` executes if no errors occur
* `ensure` executes whether or not an exception occurs
  * Goes after last rescue clause
* Example: file handling

```ruby
f = File.open("testfile")
begin
    # .. process
rescue
    # .. handle error
else
    puts "Congratulations-- no errors!"
ensure
    f.close unless f.nil?
end
```

