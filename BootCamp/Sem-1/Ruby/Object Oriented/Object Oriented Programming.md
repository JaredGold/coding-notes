# Object-Oriented Programming

#### What is Object-oriented Programming? (OOP)

It is a computer programming model that organizes software design around data, or objects, rather than functions and procedural logic.

##### Procedural Design

* Get Dog Name
* Feed Dog
* Take Dog For a walk
* Print dog daily Journal

Real top down design and one flow

##### OOP Design

You start with a dog object and 3 attributes (name, walks, meals)
You update the state of the item `dog` when it takes a walk or eats meals. You follow the properties in the object.

```ruby
class Dog
    attr_reader :name
    def initialize(name)
        @name = name
        @walks = []
        @meals = []
    end
    def walk(km)
        @walks << km
    end
    def eat(grams)
        @meals << grams
    end
    def display_daily_log
        puts "#{@name}'s day:"
        puts " ate #{@meals[0]}g of food"
        puts " walked #{@walks[0]} km"
    end
end
```



#### Principles of OOP

1. Encapsulation
   - Each object keeps it's attributes (states) private, and controls which external entities can access attributes and how they can access them by providing methods.
2. Abstraction
   - Objects provide a consistent, high-level interface for interaction, hiding the complexities of their internal structure and workings.
3. Inheritance
   - Objects can be defined in a hierarchy. Parent objects encapsulate shared attributes and actions and child objects can differentiate where needed.
4. Polymorphism
   - Meaning "many shapes" in Greek, parent objects define actions (methods) and child objects can implement those named methods in different ways according to their nature



## Benefits of OOP

- Reusable code through inheritance
  - Common attributes and actions implemented in one place
- Simple and clear interfaces through encapsulation
  - Hidden complexity with consistent interfaces
- Flexibility through polymorphism
  - One name for a method that can be implemented different ways by each child class.