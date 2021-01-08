# Ruby Classes (Inheritance and mixins)

## Inheritance

#### What is it?

* Inheritance involves using an existing class to define another class
* It creates a tree hierarchy of classes in which each class can inherit from the classes above it in the hierarchy
  * But only directly from a single class
* Child classes have access to all of the instance variables and methods up the hierarchy

##### Class Hierarchy Example

Imagine a down facing tree

- Animal
  1. WildAnimal < Animal
  2. Pet < Animal
     1. Dog < Pet
     2. Cat < Pet
     3. Bird < Pet

#### Why use it?

* It can be used to share common attributes and actions among similar types of classes
  * Reduce code duplication (DRY)
  * Facilitates modularity
  * Facilitates code reuse
  * Easier testing and maintenance



#### Syntax and Terminology

* Ruby syntax uses the symbol, `<`, to indicate a class inherits from another class

  ```ruby
  class Dog < Pet
  end
  ```

* Pet is a **superclass** of Dog, and Dog is a **subclass** of Pet

* All Ruby classes are subclass of Object, and Object is a subclass of BasicObject

  * Use `.superclass` to see the direct parent (superclass) of any class

    (Ex; `Dog.superclass` shows 'Pet')

##### Extending the Pet Class (Objects & Classes file)

* We can use the common attributes and actions for Pet (the parent class)
* For specific types of Pet, we can define subclasses (child classes) with an additional attributes and actions relevant for that type of pet

#### super

Use the `suber` method to execute the code defined in the parent class from the child method

* Important for initialize method
* May be useful for other methods implemented by the child

```ruby
class Dog < Pet
    attr_accessor :breed
    def initialize(name, breed)
        super("dog", name)		# Passes what the super class requries (Pet)
        @breed = breed
    end
end
```

#### Dogs are Pets with more

* When Dog is instantiated (when an object is created with Dog.new)

  ```ruby
  roy = Dog.new("Roy", "Lbarador")
  ```

* The instance (roy) has access to everything in Pet

  * @name, @type, eat, display_daily_log, to_s, self.total_pets

* The instance (roy) also has access to everything in Dog

  * @breed, walk

##### Example

new file called dog.rb

```ruby
require_relative('./pet')

class Dog < Pet
    attr_reader :breed
    def initialize(name, breed)
        super('dog', name)
        @breed = breed
        @walks = []
    end
    
    def walk(distance_in_kms)
        @walks << distance_in_kms
    end
    
    def display_daily_log
        super				#=> Contains all attributes from the super class
        puts "#{@name} has taken the following walks today:"
       	@walks.each do |walk|
            puts "  #{walks} kms"
        end
    end
end
```

```ruby
roy = Dog.new("Roy", 'Labrador')
puts roy								#=> 'Pet: type-dog name-Roy' 
puts '#{roy.name} has type #{roy.type}' #=> 'Roy has type dog'
roy.eat(10, "morning")

# Done before updating daily log
roy.display_daily_log					#=> 'Roy ate 1 meals today:'		
										#=> '   10 Grams in the morning'
puts "Roy's breed is #{roy.breed}"		#=> 'Roy's breed is Labrador

#Done after updating daily log
roy.walk(2)
roy.display_daily_log					#=> 'Roy ate 1 meals today:'		
										#=> '   10 Grams in the morning'
										#=> 'Roy has taken the following walks today:'
										#=> '   2 kms'

poto = Pet.new('cat', 'Poto')
poto.eat(10, "morning")
poto.display_daily_log					#=> 'Poto ate 1 meals today:'		
										#=> '   10 Grams in the morning'
```



### Polymorphism - speak method

* We can override parent methods with specific implementations in the children
* Most pets make some kind of sound but they are all different

```ruby
class Pet
    def speak
        # implemented by children
    end
end

class Cat < Pet
    def speak
        puts "Meow!"
    end
end

class Dog < Pet
    def speak
        puts "Woof!"
    end
end
```

---

```ruby
poto = Cat.new("Poto")
roy = Dog.new("Roy", "Labrador")

pets = [poto, roy]

pets.each do |pet|
    puts "#{pet.name} says:"
    pet.speak
end
```

```ruby
`Poto says'
'Meow'
'Roy Says'
'Woof'
```



## Mixins

#### Mixing in other behaviours

* On limitation  of inheritance is that we can only inherit from a single parent class
* Mixins can be used to provide extra behaviours that are common for multiple classes that don't share the same hierarchy
* Same naming convention as classes (PascalCase)
* Mixins are implemented as **modules** that are included in class definitions with the `include` keyword

```ruby
module Flyer
    def can_fly?
        true
    end
end

class FruitBat < Animal
    include Flyer
end

class Bird < Pet
    include Flyer
    def initialize(name)
        super("fish", name)
    end
end

class Jet
    include Flyer
end
```

