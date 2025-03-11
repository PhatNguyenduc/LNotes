`go build filename.go` to build a file and do ./filename to run it

`go run filename.go` to run and executes file and will NOT create an executable file in our current folder

<h3>Go Package</h3>
Projects can contain many .go files, organized into packages.Each package is like a directory: .go files to do with one part of your program can go in one package

```
package main  // package declaration

import "fmt"

func main () {
  fmt.Println("Hello World")
}

```
