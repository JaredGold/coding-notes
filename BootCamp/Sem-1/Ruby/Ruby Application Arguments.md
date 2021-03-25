# Passing command line arguments

Just like we pass arguments in methods, we can also pass command line arguments to our entire Ruby program when we execute it

`ruby myapp.rb "My Awesome App"`

### ARGV

* When a command line argument is passed to a ruby program it is stored in a special array variable called ARGV
* Arguments are separated by spaces on the command line
* Each argument will be one item in the ARGV array

```ruby
title = "Amazing App"
user = "Username"

puts "Arguments: "
puts "#{ARGV}"

puts "Welcome to #{title}, #{user}!"
```

```ruby
title = "Amazing App"
user = "Username"

title = ARGV[0] if ARGV[0]
user = ARGV[1] if ARGV[1]

puts "Welcome to #{title}, #{user}!"
```

