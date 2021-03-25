# Rspec

## What is Rspec?

* Rspec is a collection of ruby gems to test code!

Install the rspec gems

​	`gem install rspec`

---

#### Rspec-core

* Provides structure for writing tests, controls which tests are run and the format of the results
* Uses the words `describe` and `it` to express tests like a conversation

```ruby
describe 'main methods' do
    it 'should be able to add' do
    end
end
```

#### Rspec-expectations

* Used to assert expected test results
* Many built in matchers
  * Identity - `to be`, `to eq`
  * Comparisons - `to be <`, `to be >`
  * Regular expressions - `to match`
  * Types/classes - `to be_an_instance_of`, `to be_a_kind_of`
  * Truthiness - `to be_truthy`, `to be_falsy`, `to be_nil`, `to_not be_nil`
  * Errors - `to raise_error`

[READ MORE ON RSPEC-CORE](https://rubydoc.info/gems/rspec-core/frames/) - The rspec-core Docs!

[READ MORE ON RSPEC-EXPECTATIONS](https://rubydoc.info/gems/rspec-expectations/frames) - The rspec expectations docs!



#### Example

```ruby
require_relative '../pet'

describe Pet do
    it "should have a name" do
        pet = Pet.new("Poto")
        expect(pet.name).to eq "Poto"
        expect(pet.name).to match /^P/
        expect(pet).to be_instance_of Pet
    end
end
```

---

# Our made example

**Scenario: **Write a method called `largest` that will return the largest value in an array of values

1. Write tests
2. Run tests - watch them fail!
3. Write code and modify until the tests pass - yay!

---

#### Create the test file and the source file

* Create a directory called `largest` for this project
* Create a file called `largest.rb` that will contain the `largest` method
* Create a file called `largest_spec.rb` in a new `spec` directory
  * Rspec looks for test files in a `spec` directory (spec stands for speciality)

Continue running the rspec and fixing one problem at a time until it fully works

##### largest_spec.rb

```ruby
require_relative '../largest'

describe 'largest' do
 	it 'should return the largest number in an array of numbers' do
    	expect(largest([1,2])).to be 2 # or be(2)
    end
    it 'it should return the largest number when it is the second in the array' do
    	expect(largest([0,1])).to be(1)
    end
    it 'it should return the largest string' do
        expect(largest(["a", "ab"]).to eq("ab")
    end
end
```

##### largest.rb

```ruby
def largest
end
```

```ruby
def largest(values)
end
```

```ruby
def largest(values)
	return 2
end
```

```ruby
def largest(values)
	largestValue = values[0]
    values.each do |value|
        if (value > largestValue)
            largestValue = value
        end
    end
    return largestValue
end
```



