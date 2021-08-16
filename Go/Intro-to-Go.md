

# Intro to Go

---

When using Go you have the ability to check the docs on what function you are importing and using by using the command `doc` in the terminal. On example would look like `$ go doc fmt.Scan` which will show specifically the scan function imported in the package fmt.

To execute Go code we first need to build it in the terminal using `$ Go build main.go` where `main` changes depending on the name of the file being executed. We use the `package main` to declare that file will be compiled into an executable file. 

Below is an example of a `Hello World` application using Go.

```go
package main

import "fmt"

func main(){
  fmt.Println("Hello World!")
}
```

#### Array + Slice

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

#### Loops

Creating a `for` loop inside of go is very similar to JavaScript. First we declare a for with either one or two variables. Then we assign it to a range with the array or slice. At that point it is like any other for loop.

```go
func main(){
  fruits := []string{"Apple", "Pear", "Banana"}
  
  for i, fruit := range fruits {
    fmt.Println(i, fruit)
  }
}
```



