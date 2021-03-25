# Arrays

#### What is an Array

* An array is a collection of items (like a folder)
* While defining values to a variable, similar kind of data can be grouped together

``` ruby
educators = ["Jim", "Pam", "Soozi", "Bianca"]
```

* An array can hold any data type: integer, string, etc.
* Arrays can also hold multiple different data types.
* Arrays can also hold arrays (2D Array)

```ruby
array_test = [1, 1.0, ["Mike", false, x]]
```

#### Accessing an Array

* An array always starts at 0 not 1
* If a value does not exist in an array position it returns `nil`
* Negative index can be used to access elements from the reverse end. `-1` in an array that has 4 values would start at value `3` instead of `0`

## Array Methods

* Array has a whole bunch of predefined methods to access and manipulate array elements
* Few methods are
  * `length` - counts total items in array
  * `join` - combines all items into one single word
  * `include?` - checks if item exists in array
  * `delete` - deletes all of given value from the array
  * `delete_at` - deletes a particular element at said position
* [ARRAY DOCS](https://ruby-doc.org/core-2.7.0/Array.html)

```ruby
educators = ["Jim", "Pam", "Soozi", "Bianca"]

educators.length 			# => 4

["a", "b", "c"].join 		# => "abc"

educators.include?("Mike")	#false
educators.include?("Jim")	#true

a = [ "a", "b", "b", "b", "c"]
a.delete("b")
a							# => ["a", "c"]

a.delete_at(3) 				# => [ "a", "b", "b", "c"]
```

---

### Array Mutation

* Array is pass by reference (points to memory location) and not pass by value unlike strings

If you change an array it will change the value of all the array's that are pointing to that array.

* If you want to make a copy of an array you need to clone it.

```ruby
names = ["Jared", "Kim", "Ezra"]
copy_names = names.clone				# => Makes a brand new array called copy_names
test_names = names						# => Still points to names so if we change names we change test_names
```

---

## Error handling in Arrays

* Errors always stop a program. - Not good to have in live app
* Errors are always good for debugging though.
* While applying methods on array elements, a short circuit logic should be used to check if the value exists on then should the method be applied

```ruby
names = ["jared", "kim", "ezra"]
names[0].capitalize				#"Jared"
names[3].capitalize				#error

names[3] && names.capitalize 	#nil
```



## Multi Dimension Arrays

A multi dimension array is an array inside of an array.

```ruby
odd_even = [[1,3,5,7,9] , [2,4,6,8]]
p odd_even[0] 				# [1,3,5,7,9]
p odd_even[0][3]			# 7
```

