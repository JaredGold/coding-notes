# Here is a list of interfaces examples

## Basic Example

```go
package main

import "fmt"

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
	// VERY custom logic for generating an english greeting
	return "Hi There!"
}

func (sb spanishBot) getGreeting() string {
	// VERY custom logic for generating an spanish greeting
	return "Hola!"
}
```

In the above example we have created an interface which is shared between anything that has a function called `getGreeting` that takes a `string` it prints out the response that it gets from the `getGreeting` function using a `printGreeting` function which takes a `bot`. This was our first example.

## Shapes

```go
package main

import "fmt"

type shape interface {
	getArea() float64
}

type square struct{ sideLength float64 }
type triangle struct{ height float64; base float64 }

func main() {
	s := square{sideLength: 12.189}
	t := triangle{height: 1.89, base: 10.369}

	printArea(s)
	printArea(t)
}

func printArea (s shape) {
	fmt.Println("This shape has an area of:", s.getArea())
}

func (s square) getArea() float64 {
	return s.sideLength * s.sideLength
}

func (t triangle) getArea() float64 {
	return 0.5 * t.base * t.height
}
```

In the above code we have created two types that are fundamentally different, have a method called `getArea` which returns the area of the shape. The interface `shape` then has a function it can use called `printArea` that takes a shape and prints a line showing the size of the area.

## Read Http Request

```go
package main

import (
	"fmt"
	"io"
	"net/http"
	"os"
)

type logWriter struct{}

func main() {
	resp, err := http.Get("https://icanhazdadjoke.com/")
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(1)
	}
	
	lw := logWriter{}

	io.Copy(lw, resp.Body)

	// bs := make([]byte, 99999)
	// resp.Body.Read(bs)
	// fmt.Println(string(bs))
}

func (logWriter) Write(bs []byte) (int, error) {
	fmt.Println(string(bs))
	fmt.Println("------%%---------%%---------%%------")
	fmt.Println("Just wrote this many bytes:", len(bs))
	fmt.Println("------%%---------%%---------%%------")
	return len(bs), nil
}
```

The above code was written as a method to do a `Get` request and print the html it received back.

## Read File (`Echo`)

```go
package main

import (
	"fmt"
	"io"
	"os"
)

func main() {
	if len(os.Args) < 2 {
		fmt.Println("File not received as an argument.")
	}

	f, err := os.Open(os.Args[1])

	// if an error has occursed print error and exit
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(1)
	}
	
	// Read more on Copy and Stdout (save file to byte slice, convert byteslice to string, Print that line)
	io.Copy(os.Stdout, f)
}
```

The above code (my favorite yet) is an application that, when run accepts an argument and reads the file given and prints it's content to the terminal.

