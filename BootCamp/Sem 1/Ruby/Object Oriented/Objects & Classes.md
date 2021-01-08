# Objects and Classes

#### What is a class?

Classes are a structure that is implemented across programming languages. Ruby handles classes slightly differently

* Classes are blueprints for an object
* Define what attributes an object has and what actions it can perform

##### Example: Pet Class

Attributes

* Type
* Name
* Color
* Breed
* Size

Actions

* Speak
* Walk
* Sleep
* Eat

#### Parts of a class definition

1. Initialize method
2. Instance variables
3. Methods

### Initialize Method

* Invoked when object is created (instantiated) from class with the `new` keyword
* Used to assign initial values to the class attributes for the object
* Performs any other required initialization for the class

```ruby
def initialize
    
end
```

### Instance Variables

* Used to store **attributes** of the object
* Initialised in the initialize method
* Available to all methods defined in the class (global scope within the class definition)

```ruby
def initialize(name)
    @name = name
end
```

### Methods

* Define the **actions** that can be performed by objects of this class
* Can also be helper methods used in the class definition
* Have access to all instance variables

```ruby
def greet
    puts "Hi! My name is #{@name}"
end
```



### Pet Class Example

Making a folder called petclass and a single file called pets.rb

pets.rb ==

```ruby
# attributes: 
#	type
#	name
#	meals

class Pet
    def initialize(type, name)
        @type = type
        @name = name
        @meals = []
    end
    
# Methods the Pet class can use
    
    def eat(grams, time_of_day)
    # time_of_day is one of morning, afternoon, evening
    	@meals << {amount: grams, time: time_of_day}    
    end
    
    def display_daily_log
       puts "#{@name} ate #{@meals.length} meal/s today:"
       @meals.each do |meal|
           puts "   #{meal[:amount]} grams in the #{meal[:time]}"
       end
    end
        
    def to_s				# Overrides to_s (puts) and shows this when you put it.
        return "Pet: type-#{@type} name-#{@name}"
    end
end
```

``` ruby
dog = Pet.new("dog", "Marshall")
dog.eat(10, "morning")
dog.eat(15, "evening")
puts dog 					#=> "Pet: type-dog name-Marshall"
dog.display_daily_log 		#=> "Marshall ate 2 meal/s today:"
							#=> "   10 grams in the morning"
							#=> "   15 grams in the evening"
```



## Attribute Access

#### Setters and Getters

- Used to give access to instance variables outside of the class
- Allows the object to control access to its attributes
- should always follow **principle of least privilege**
- Setting can be dangerous to the end user for example if they change meals from an array to a string

```ruby
# getter
def name
    @name
end

# setter
# Updates a new value to the instanced variable
def name= (name)
    @name = name
```



#### `attr_reader`, `attr_writer`, `attr_accessor`

* Getters and setters for attributes are such a common pattern that Ruby has a shortcut
* `attr_reader` - read access (getter)
* `attr_writer` - write access (setter)
* `attr_accessor` - read and write

attr requires you to use symbols `:symbol` as apposed to `@symbol` or `symbol`

```ruby
# provides setter andd getter
# for @name and @type

attr_accessor :name, :type
```



```ruby
class Pet
    attr_reader :type
    attr_accessor :name
    def initialize(type, name)
        @type = type
        @name = name
        @meals = []
    end
    
    def eat(grams, time_of_day)
    	@meals << {amount: grams, time: time_of_day}    
    end
    
    # def name			# If you call dog.name it will now return the @name
    #     @name			# Not the best way to do this because it will require a lot
    # end				# for many attributes (this is why we use the attr shortcuts)
    
    # def name= (name)	# Alternate attr added up top
    #     @name = name
    # end
    
    def display_daily_log
       puts "#{@name} ate #{@meals.length} meal/s today:"
       @meals.each do |meal|
           puts "   #{meal[:amount]} grams in the #{meal[:time]}"
       end
    end
        
    def to_s			
        return "Pet: type-#{@type} name-#{@name}"
    end
end
```

```ruby
dog = Pet.new("dog", "Marshall")
dog.eat(10, "morning")
dog.eat(15, "evening")
puts dog 					#=> "Pet: type-dog name-Marshall"
dog.display_daily_log 		#=> "Marshall ate 2 meal/s today:"
							#=> "   10 grams in the morning"
							#=> "   15 grams in the evening"

puts dog.name 				#=> "Marshall"  -> this is because we gave ot the attr_reader

#before creating a setter attribute
dog.name = "Roy"		#=> Because there is no write permission this will return an error

#after creating a setter attribute or attr_accessor
dog.name = "Roy"		#=> dog changes name from Marshall to Roy

```



## Class variables and methods

#### What are they and why

* Belong to the class (the template),  not the object (the instance)
* Used for attributes and actions that are related to all elements of the class (not to a single instance)
* Class methods can be used to track and operate on all instances of a class
  * Use class methods to access class variables

##### Example - total pet count

* Class variables are defined with `@@`
* Class methods are defined with `self.method_name`

```ruby
@@total_pets = 0
def self.total_pets
    @@total_pets
end
```



CREATING A NEW FILE CALLED petstore.rb

```ruby
require_relative("./pets")

pet_store = []

# add a dog to the petstore
pet_store << Pet.new("dog", "Marshall")
# add a cat to the petstore
pet_store << Pet.new("cat", "Miles")
```

*Example of what we can already do*

```ruby
pet_store.each do |pet|
    puts pet
end

#=>"Pet type-dog name-Marshall"
#=>"Pet type-cat name-Miles"
```

*Adding to the pets.rb file*

```ruby
class Pet
    attr_reader :type
    attr_accessor :name
    @@total_pets = 0
    
    def initialize(type, name)
        @type = type
        @name = name
        @meals = []
        @@total_pets += 1
    end
    
    def self.total_pets
        @@total_pets
    end
# More below... (as above)
```

*Example of counting pets*

```ruby
pets "The store currently has #{Pet.total_pets} pets"
#=>"The store currently has 2 pets"
```



## Naming Conventions

#### Popular naming conventions

* Class names are PascalCase (each word, including first, begins with a capital letter; no underscores)
* Method names are snake_case