

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

