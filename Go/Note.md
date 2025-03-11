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

`func` to create function 
`import` package:
  <ol>
    <li>import "package 1"</li> 
    <li> or import ( "package1" 
                  "package2"
                ) </li>
      <li>alias: import (p1 "package1") so can call func from p1 `p1.Somefunc()`</li>
  </ol>
  Note: hình như các hàm trong thư viện default của Go đều viết hoa
        fmt là thư viện chủ yếu io trong Go, syntax như C viết hoa chữ đầu

If the code is being used in production (users are interacting with it) then using an executable file is preferred.


```
 f.Println("      `.-::::::-.`")
  f.Println("   .:-::::::::::::::-:.")
  f.Println("  `_:::    ::    :::_`")
  f.Println("   .:( ^   :: ^   ):.")
  f.Println("   `:::   (..)   :::.")
  f.Println("   `:::::::UU:::::::`")
  f.Println("   .::::::::::::::::")
  f.Println("   O::::::::::::::::O")
  f.Println("   -::::::::::::::::-")
  f.Println("   `::::::::::::::::`")
  f.Println("   `::::::::::::::::`")
  f.Println("      oO:::::::Oo")
```

```
      `.-::::::-.`
  .:-::::::::::::::-:.
  `_:::    ::    :::_`
   .:( ^   :: ^   ):.
   `:::   (..)   :::.
   `:::::::UU:::::::`
   .::::::::::::::::.
   O::::::::::::::::O
   -::::::::::::::::-
   `::::::::::::::::`
    .::::::::::::::.
      oO:::::::Oo

```
