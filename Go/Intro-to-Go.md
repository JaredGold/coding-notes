

# Intro to Go

---

When using Go you have the ability to check the docs on what function you are importing and using by using the command `doc` in the terminal. On example would look like `$ go doc fmt.Scan` which will show specifically the scan function imported in the package fmt.

To execute Go code we first need to build it in the terminal using `$ Go build main.go` where `main` changes depending on the name of the file being executed. We use the `package main` to declare that file will be compiled into an executable file. To simply run the file without building use `run` or `$ go run main.go` if there are multiple files required to run that file you can use `go run main.go second.go third.go`.

Below is an example of a `Hello World` application using Go.

```go
package main

import "fmt"

func main(){
  fmt.Println("Hello World!")
}
```

## Array + Slice

In Go there is a difference between creating an array and a slice. An array has a prefixed length but can hold any type, where a slice has an endless size but can only hold one type. With creating two there are some major differences.

```go
// ~~~ Array ~~~
var a [2]string	// array with length of 2 holding strings
a[0] = "Hello"
a[1] = "World"
	// or
primes := [6]int{2,3,5,7,11,13}

// ~~~ Slice ~~~
var b []string
b[0] = "Hello"
b = append(b, "World")
	// or
primeNumbers := []int{2,3,5,7,11,13}
```

### Slice Range Syntax

To select a range of values in a slice is very similar to Javscript and other languages. In Go we use `varName[startIndexIncluding : upToNotIncluding]` for example if we had a range of integers counting up and we wanted from 1 to 5 (including 5) we would use `nums[0:5]` this would return us `[0-4]`. Optionally we can not give the first or second number in the range to say from the begining or to the end. So as above `nums[:5]` would do the same. If I wanted to select a range up to the end it would be `nums[0:]`.

### Array Join

To join an array/slice we can use the `string` package and use a `Join` function. It is used as `String.Join([]string something, string "seperator")`. The seperator is the value used to seperate each joined string ("," " " "-")

### Array Length

To get the length of an array or slice we dont use dot notation but instead use the function `len()`. `len` takes the slice and returns an integer value. `len([]int{1,2,3})` = `3`

## Loops

Creating a `for` loop inside of go is very similar to JavaScript. First we declare a for with either one or two variables. Then we assign it to a range with the array or slice. At that point it is like any other for loop.

```go
func main(){
  fruits := []string{"Apple", "Pear", "Banana"}
  
  for i, fruit := range fruits {
    fmt.Println(i, fruit)
  }
}
```

If in a loop, or other use cases, you don't want to use the `i` variable it can be replaced with `_` which states 'I know there is a variable there I just don't need it'

## `type`

To create a new type we use the keyword `type` followed by the name of the type and anything it extends by. `type deck []string` for example creates the type deck which extends the `string slice` type.

### Type Functions

To create a function attached to a type we create a function in the same file, this function will look different as shown `func (var type) name(){}`. Breaking it down we pass a variable to be used inside the function then the type that will have access to this function, followed by our regular syntax. The best way to visualise the `var` is like `this` in javascript. The `var` is conventionally a single character that represents the first char of the type. This can be demonstrated below:

```go
type deck []string

func (d deck) print() {
	for i, card := range d {
		fmt.Println(i, card)
	}
}
```

## Functions

As above, to create a function we use the `func` keyword followed by the name of the function, round brackets and curly brackets. There can be some slight differences between a simple function, a function that returns a single variable, a function that returns multiple values anda function assigned to a type. In order to create a function that returns a value we do so by writing the return type after the set of round brackets as so:

```go
func maths(num1 int, num2 int) int {
  return num1 + num2
}
```

If a function needs to be assigned to a type we pass the type and new variable name before the name of the function.

```go
func (f food) eat() {
  fmt.Println("You ate " + f)
}
```

Finally if we want a function to return multiple values we do so by placing the two types at the end of the final round bracket in a set of their own round brackets. To set the return variable to variables after it is called we do so by splitting the assigned variables with a comma

```go
func calculate(num1 int, num2 int) (int, int) {
  return num1 + num2, num1 - num2
}

add, sub := calculate(8, 32)
```

## Type Conversion

If we have something of one type and we want to change it to another type we can do so quite easily. In go to convert a type all we have to do is use the type with a round bracket and inside that bracket what we have to change. `string(32)` == `"32"` or `[]byte("Hi there!")`

## If

If statements are very similar to other languages.

```go
if x != nil {
  // do something
}
```

## Testing

To create a test first we create a file that has a name then `_test.go` or `deck_test.go`. To run this test we use the command `go test`. To create the test it is important first that the package is the same as the functions it is testing. After this we create the testing function which takes the function you are testing and puts `Test` infront of it, It is also important that this function is written in `PascalCase`. Then in the round brackets we pass `(t *testing.T)`.

```go
package main

import "testing"

func TestNewDeck(t *testing.T) {
	d := newDeck()

	if len(d) != 52 {
		t.Errorf("Expected deck length of 52, but got %v", len(d))
	}

	if d[0] != "Ace of Spades" {
		t.Errorf("Expected first card to be \"Ace of Spades\", but got %v", d[0])
	}

	if d[len(d) - 1] != "King of Clubs" {
		t.Errorf("Expected last card to be \"King of Clubs\", but got %v", d[len(d) - 1])
	}
}
```

## Struct (Object)

Struct is short for Data Structure. That structure can hold multiple key value pairs. This is very similar to JavaScripts Objects or Ruby's Hash. None of the previous are exactly the same as a Struct but they are extremely similar. To create a struct we first need to declare the type. We do this by using `type name struct` where name is changed to the name of the structure. It is followed by curly brackets and then the properties are passed in.

```go
type person struct{
  firstName string
  lastName string
}
```

If you then want to create a person there are multiple methods. One way is as below:

```go
alex1 := person{"Alex", "Anderson"}	// 1
alex2 := person{firstName: "Alex", lastName: "Anderson"}	// 2

var alex3 person
alex3.firstName = "Alex"
alex3.lastName = "Anderson"
```

Although the first method works it is not safe, It is strongly reccomended you use the second approach.

## Maps (Object)

A map is a collection of key value pairs. It is absolutely similar to a Hash, Object or Dictionary in Ruby, Javascript and Python. With a map all keys must be of the same time and all values must be of the exact same type, this is what differentiates it to structs. There are again multiple ways to create a map. The literal way is assigning a variable the type `map` then followed with `[type]type{}` in the curly brackets we put the key value pairs, same as you would in JS.

```golang
colors := map[string]string{
	"red": "#FF0000",
	"green": "#4bf745",
}
```

There are two other ways to declare and assign maps would be by assigning it to a variable like we would other vars `var colors map[string]string` or again you could use `colors := make(map[string]string)`. Of all the ways I believe the top variant is best use if the map already has things needed to be into it.

To push a key value pair into a map you do so similar to other languages, you call the variable followed by square brackets holding the key and then what it equals. `colors["white"] = "#FFFFFF"`. Unlike structs you can not create a key value pair with dot point notation, this is because it is strongly typed. 

If you want to delete an item from the map it is quite easy, you use the function `delete()` and inside the brackets the first argument is the variable holding the map and the second variable is the key you want to delete. `delete(colors, "white")`.

To create a function that uses a map is slightly different (logically) to how we create a regular function in golang. First in the type we are passing in it will always be `map[type1]type2`. If we want to then use a loop over it we can use the first variable being the `key` and the second value being the `value`. 

```go
func printMap(c map[string]string){
	for color, hex := range c{
		fmt.Println(color +" : "+ hex)
	}
}
```

On major difference between a map and a struct is that a struct has predefined keys where a map can add more keys after run time.

## Pointers

A pointer is commonly used in C, C++ and other memory focused languages. It simplified is a way to point specifically to a location in the memory (RAM). Go is a pass by value language, this means that whenever we pass a value into a function go takes the value and copies all of the data into another location in memory. So when we want to modify data using a function it will simply point to a new location in memory and update the **<u>COPY</u>** that means that the original is not affected. This is why pointers are very important in go. So to create a pointer we use a `&` to say this variables memory. Alongside that if we want to access the values inside of the pointer we use `*`. If we want to update something in that memory point in a function we use the `*pointer` as the TYPE in our function.

```go
type person struct{
  firstName string
  lastName string
  age int
}

func main() {
  jared := person{
    firstName: "Jared",
    lastName: "Jaredstein",
    age: 27
  }
  
  jaredPointer := &jared	// this pointer directly points to the memory location of the jared struct.	
  jaredPointer.updateName("Mike")
  
  func (pointerToPerson *person) updateName(newFirstName string) {		//  the type is not person but a type of pointer that points to person.
		(*pointerToPerson).firstName = newFirstName	// pointerToPerson is wrapped in round brackets to then reference what it is pointing TO
	}
}

```

The easiest way to understand is you can turn a memory `address` into a `value` with `*address`, or turn a `value` into `address` with `&value`.

The side thing to know is that if I wanted to do the same thing I don't have to use `&` and make a pointer as go will automatically turn your pointer of type person to be exactly what you need. This makes coding simpler but it is important to still use `*` with the functions.

```go
jared.updateName("Mike")
  
func (pointerToPerson *person) updateName(newFirstName string) {		//  the type is not person but a type of pointer that points to person.
  (*pointerToPerson).firstName = newFirstName	// pointerToPerson is wrapped in round brackets to then reference what it is pointing TO
}
```

### Data Types (Val vs Ref)

With data types some are the data stored in memory and others are the references to the point in memory. The Value's all require pointers *(see above)* where reference types can be updated as they only change where they are refering to.

| <u>Value Types</u> | <u>Reference Types</u> |
| ------------------ | ---------------------- |
| int                | slices                 |
| float              | maps                   |
| string             | channels               |
| bool               | pointers               |
| structs            | functions              |

## Interfaces

An interface is a way of creating a type that anything that can match it's criteria can be an honorary type of that. For instance if I created 2 boths that spoke english and spanish, which both had their own individual function called `getGreeting()` and that function returned a string, I could create an interface which is looking for anything with a function called `getGreeting()` and returns a string. So both the spanish both and english bot would be of that new type. This allows us to create functions which is looking for the type `bot` instead of `englishBot` and `spanishBot`. We use interfaces to define a function set. You can make it strictly require a function that returns a specific type AND/OR the argument types.

```go
type bot interface {
	getGreeting() string
}

type englishBot struct{}
type spanishBot struct{}

func main() {
	eb := englishBot{}
	sb := spanishBot{}

	printGreeting(eb)
	printGreeting(sb)
}

func printGreeting(b bot) {
	fmt.Println(b.getGreeting())
}

func (eb englishBot) getGreeting() string {
	return "Hi There!"
}

func (sb spanishBot) getGreeting() string {
	return "Hola!"
}
```

Some interfaces to know and look into are Writer, Reader and Copy (in golang docs under `pkg`)

```go
package main

import (
	"fmt"
	"io"
	"net/http"
	"os"
)

func main() {
	resp, err := http.Get("https://icanhazdadjoke.com/")
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(1)
	}

	io.Copy(os.Stdout, resp.Body)

	// bs := make([]byte, 99999)
	// resp.Body.Read(bs)
	// fmt.Println(string(bs))
}
```

## Go Routines and Channels

When creating code sometimes we want actions to run at the same time (synchronous), we do this using go routines, this is normally because we have something blocking us like a `Get` request. To create a new go routine all you have to do is before the function that will be blocking is called add the word `go` before it. `go checkLink(link)`. The way this works in more detail is there are sub routines created that run in parallel to the main routine, the issue with this is that if the main routine finishes before the children routines (coroutines) finish then the app simply closes. In order to fix this problem we can create a channel. A channel will communicate between all go routines, there is no other way to communicate between each routines without it.

In order to create a channel we do this by following the same patterns as if we created any variable, the key with creating channels is it takes a type (`string, int, float`). So a basic channel would look like `c := make(chan string)`. Then when we want to use our channel we can pass it into functions and use it as `c chan string` in our function variables. When we want to either send or receive data through a channel we need to use special syntax. This sytnax is an arrow `<-` which points either value into channel or channel into variable or channel into function

```go
channel <- 5 // send the value 5 into the channel
myNum <- channel // wait for a value to be sent into the channel then assign that value to myNum
fmt.Println(<- channel) // wait for a value to be sent into the channel. When we get one log it out immediately
```

We still are not done here. When you run code and push something into channel it should near immediately exit. The reason for this is due to channels being a blocking action as well. The moment a routine finishes the main routine starts back up and if there is nothing else to run it then ends and exits the program.

Below is an example of a go routine and a channel working to check if websites are currently up.

```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

func main() {
	links := []string {
		"http://google.com",
		"http://facebook.com",
		"http://amazon.com",
		"http://golang.org",
		"http://stackoverflow.org",
	}	

	c := make(chan string)

	for _, link := range links {
		go checkLink(link, c)
	}

	// this is an infinite loop (!CAUTION!)
	for link := range c {
		go func(l string) {
			time.Sleep(3 * time.Second)
			checkLink(l, c)
		}(link)
	}
}

func checkLink(link string, c chan string) {
	_, err := http.Get(link)
	if err != nil {
		// color red
		fmt.Println("\033[31m", link, "might be down!")
		c <- link
		return
	}
	// color green
	fmt.Println("\033[32m", link, "is up!")
	c <- link
}
```

