# Iterators

## What is an Iterator

* Hashes and Arrays are both known as collections.
* Collections have multiple predefined methods which allow us to iterate over them
* These methods are iterators

```ruby
collection.each do |variable|		# Good for multi line code
    code
end

collection.each {|variable| code}	# Good for one line code
```

#### Blocks

* A block is the code between the variable and end

### Each

* `each` method iterates through every element in the collection and executes the code block
* Each iterator for an array takes one argument where as has takes two arguments

```ruby
array.each do |item|				# Array
    code
end

hash.each do |key, value|			# Hash
    code
end
```



### Each_With_Index

* `each_with_index` is similar to the each method although it can take two arguments from an array : value of an array item and it's index.
* It takes three elements for a hash

```ruby
array.each_with_index do |item, index|
    code
end

hash.each_with_index do |(key, value), index|
	code
end
```



### Map

* `map` is similar to each but it creates a brand new array from the values returned by the block

```ruby
numbers = ["one", "two", "three"]

numbers_uppercased = numbers.map do |item|
    item.upcase
end
```

### Filter / Select

* `select` returns a new array containing truthy results

```ruby
[1,2,3,4,5].select do |num|
	num.even?
end

# [2,4]
```

