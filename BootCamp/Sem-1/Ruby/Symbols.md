# Symbols

#### What is a Symbol?

* Symbol is another data type used in ruby.
* Symbol looks like a string but is represented with `:` at the front
* Symbols are not strings
* They Point to the same memory location once it is created
* String constantly points to a different memory location

```ruby
x = :hello
```



#### Why use a symbol

* Symbols are faster to use because they use the same memory location
* Strings are created each time, but symbols are stored once in the memory
* It is just like a label, hence symbols are best to used in data types (**<u>GREAT</u>** for hashes)

#### Syntax

* A symbol can not be a number but it can be a character

#### Difference between symbol and String

* String is a text that can be called and used in concatenation
* Symbol is a symbol or a label and thus can't be concatenated