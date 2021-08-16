# Ruby

## Basics

* `puts` prints whatever it is.
* to run a ruby program in console (in the right folder) `ruby program.rb`
* You can `*` (times) a string to write the string multiple times
* You can save a *variable* with it's value (*assignment*) as below. The first character needs to be a lowecase letter.

```ruby
myString ='...you can say that again...'
puts myString
```

* To change a value to a string we use `.to_s`

* To change a value to an integer use `.to_i`

* To change a value to a float we use `.to_f`

  ```ruby
  var1 = 2 			#int
  var2 = '2'			#string
var3 = 1.97			#float
  
  puts var1.to_s		#change to string	(and print)
  puts var2.to_f		#change to float	(and print)
  puts var3.to_i		#change to int		(and print)
  ```
  
* The reason `puts` will print floats is because it is automatically converting it to a string (thats what the s in puts is for)

* `gets` gets a string from the user.

  ```ruby
  puts 'Hey what\'s your name?'
  name = gets
  puts 'Hey there, ' + name + ' nice to meet you.'
  ```

* When the above code is run it leaves a return after the users name, this is because the gets command got the return when returning your name. To get rid of that return we use `.chomp` 
  The above code would look like this `name = gets.chomp`
  
* `self` points to the object you are currently in. For example well calling `puts` what you are really calling is `self.puts`

* 