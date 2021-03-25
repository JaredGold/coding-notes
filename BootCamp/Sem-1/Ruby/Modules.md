# Modules

#### What is a module

A module is a group of objects under a module name

Objects in a module can include

* Methods
* Classes
* Constants
* Other Modules

#### Why Modules

* Reusability
  * Can provide methods, classes and constants used by multiple applications or application components
* Provide a <u>namespace</u>
  * Prevent name clashes
* Enables Mixins
  * Used by classes to implement multiple inheritance

## Namespaces

When a module is used to group objects it is referred to as a namespace

Namespaces are used in the Ruby Standard libraries to avoid cluttering the main Kernel namespace

#### Why namespaces?

When you create your own modules, the namespace of your module will prevent name clashes in your programs.

* You use the name of your module to explicitly refer to objects from that module

Prevents using another object(method, module, class or constant) with the same name accidently

## Module Syntax

* Define a module with the `module` and `end` keywords
* Use module name with "." to define methods

```ruby
module MyLogger
    SEPERATOR = "**-------**"
    def MyLogger.info(message)
        puts "#{message}"
    end
    def MyLogger.warning(message)
        puts "WARNING -- #{message}"
    end
        def MyLogger.error(message)
        puts "WARNING -- #{message}"
    end
    class Debugger
        attr_reader :env
        def initialize(env)
            @env = env
        end
        def debug(content)
            MyLogger.info("#{@env}: #{content}")
        end
    end
end
```



#### How to use the module

* Use module name with `.` to refer to module methods
* Use module name with `::` to refer to classes and constants

```ruby
MyLogger.info("An informational message")
puts MyLogger::SEPARATOR
MyLogger.warning("A warning")
puts MyLogger::SEPARATOR
MyLogger.error("Danger Will Robinson")

debugger = MyLogger::Debugger.new("test")
debugger.debu("debugging message")
```

