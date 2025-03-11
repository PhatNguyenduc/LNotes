cơ bản thì syntax và các kiểu dữ liệu như C (không `;`)
```
package main

import "fmt"

func main() {

    fmt.Println("go" + "lang")

    fmt.Println("1+1 =", 1+1)
    fmt.Println("7.0/3.0 =", 7.0/3.0)

    fmt.Println(true && false)
    fmt.Println(true || false)
    fmt.Println(!true)
}
```

**Khai báo biến bằng var.**

Syntax: var <name> <kiểu dữ liệu> = <value> eg:`var b, c int = 1, 2`
        gán trực tiếp có thể không cần định kiểu  ` var a = "initial" `
        shorthand: `f := "apple"` <=> `var f string = "apple"`


Go supports constants of character, string, boolean, and numeric values.  
` const s string = "s"`

**for loop** :forloop không có mở ngoặc 😃; có nhiều cách viết for loop trong Go 
```
    //1
    i := 1
    for i <= 3 {
        fmt.Println(i)
        i = i + 1
    }
    //2
    for j := 0; j < 3; j++ {
        fmt.Println(j)
    }
    //3
    for i := range 3 {
        fmt.Println("range", i)
    }
    //4
    for {
        fmt.Println("loop")
        break
    }
  
    for n := range 6 {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }
}
```

**if-else** trong go cũng vậy nhưng khác C ở chỗ có thể gán biến thẳng vào conditional vd: 
`
if num := 9; num < 0 {
        fmt.Println(num, "is negative")
    }
`
biến được gán chỉ tồn tại trong hết câu lệnh if-else

**switch-case**
Tương tự thế
```
t := time.Now()
    switch {
    case t.Hour() < 12:
        fmt.Println("It's before noon")
    default:
        fmt.Println("It's after noon")
    }
```

Một ví dụ ở đoạn này là hàm có thể đặt tên gán thành biến như JavaScript:
```
    whatAmI := func(i interface{}) {
        switch t := i.(type) {
        case bool:
            fmt.Println("I'm a bool")
        case int:
            fmt.Println("I'm an int")
        default:
            fmt.Printf("Don't know type %T\n", t)
        }
    }
whatAmI(true)
    whatAmI(1)
    whatAmI("hey")
```
OUTPUT:
```
I'm a bool
I'm an int
Don't know type string
```
