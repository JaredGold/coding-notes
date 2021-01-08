# Hashes

### What is a hash?

* Hash is a ruby data type used to define a collection of **Key Value Pairs**
* If we want to define a phone directory with names and their corresponding number we would use a hash
* Hash is more useful then two arrays

```ruby
names = ["Bob","Charlie", "Peter"]
contact_no = ["1234567890", "0123456789", "9012345678"]
# ^^ This is not good because there is no way to link number to name ^^

phone_book = {"Bob" => "1234567890", "Charlie" => "0123456789", "Peter" => "9012345678"}
# ^^ They link a name to a number ^^
```



### Syntax

```ruby
test = {:Key => "Value", :Second_Key => "Value"}
```

* It is preferred to use a symbol/label then a string although it could be either
* Value's could be of any data type
* To call a value you do so as below

```ruby
test[:Key] 		# Would show the value marked by :Key symbol
```

#### Alternate Syntax

* Alternate syntax with **no fat arrow key** would be to place the colon at the front

```ruby
{:key => "value"}
#Shorthand / Alternate Syntax
{key: "value"}
```



### Accessing Hash Elements

* Hash elements are accessed using it's key names
* If a key accessed does not exist it returns nil
* Keys in a hash could be a symbol or string
* If a key is a string it must be accessed a key

```ruby
profile[:key]
profile["key"]
```



### Hash Methods

* Hash has a a bunch of methods to access and manipulate Hash elements easily
* Some of these methods are
  * keys - prints out the keys
  * values - prints out the values
  * include? - checks if there is a key with the name give
  * length? - checks the length of the hash

[Hash MDN](https://ruby-doc.org/core-2.7.0/Hash.html)

```ruby
profile = {name: "Peter", age: 20, title: "Painter"}

profile.keys 			#=> [:name, :age, :title]

profile.values 			#=> ["Peter", 20, "Painter"]

profile.include?(:name) #=> true
profile.include?(:bio) 	#=> false

profile.length 			#=> 3
```

