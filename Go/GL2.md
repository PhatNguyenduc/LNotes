<h1>Map</h1>  
To create an empty map, use the builtin make: make(map[key-type]val-type)  

` m := make(map[string]int)`  
như map trong các ngôn ngữ khác không khác biệt  
lấy value bằng `[key]` ví dụ map trên `m[k1] = 7`  
nếu key không tồn tại nó đc gán giá trị *Zerovalue* cho kiểu dữ liệu của nó.  
Tiện đây nói luôn về zerovalue trong Go: `false` cho *booleans*, `0` cho các loại số, "" cho *String* và `nil` cho pointer,functions, interfaces, slices, channels, and maps.  
lệnh `delete` remove 1 cặp (key,val) khỏi map. Để remove all thì dùng `clear`   

<h1>Multiple Return type value</h1>  

Go has built-in support for multiple return values.  
Chả biết diễn giải như nào cho hay, nhìn ví dụ thì hiểu liền. Nói chung lúc khai báo thì khai báo nhiều kiểu giá trị trả về là được.  
```
func vals() (int, int) {
    return 3, 7
}
a, b := vals()
_, c := vals()
```
Nếu không muốn dùng giá trị nào thì dùng blank `_` là được.   

<h1> Vadiaric Function</h1>  
Trong Go, Variadic Functions là các hàm có thể nhận một số lượng tham số không xác định của cùng một kiểu dữ liệu.  

```
func sum(numbers ...int) int {
	total := 0
	for _, num := range numbers {
		total += num
	}
	return total
}
```
nói chung chả thấy hay ho gì cái này lắm cứ cho vào mảng cũng được, không thấy tối ưu hơn lắm(?) flex hơn.  
Truyền cả slide hay các thứ dạng mảng thì doc dạy thế này:  
If you already have multiple args in a slice, apply them to a variadic function using `func(slice...)` like this.  

<h1>Closures</h1>  
Đọc hướng dẫn xong thấy code chả hiểu lấy ví dụ kiểu gì. 
Có thể hiểu Closures là hàm ẩn hay hàm lồng nhau. Có thể truy cập và duy trì trạng thái của các biến bên ngoài phạm vi của nó ngay cả sau khi hàm bên ngoài đã thực thi xong.  
💡 Nói cách khác: Closure giúp một hàm "nhớ" các biến của môi trường nơi nó được khai báo.

2 ví dụ dễ hiểu từ gpt:  
1.Cơ bản Closures
```
package main

import "fmt"

func counter() func() int {
	count := 0
	return func() int { // Đây là một closure
		count++
		return count
	}
}

func main() {
	nextNumber := counter() // nextNumber là một closure

	fmt.Println(nextNumber()) // 1
	fmt.Println(nextNumber()) // 2
	fmt.Println(nextNumber()) // 3
}
```
2. Closure sử dụng nhiều biến
```
package main

import "fmt"

func adder(x int) func(int) int {
	return func(y int) int {
		x += y
		return x
	}
}

func main() {
	add5 := adder(5)  // Tạo một closure bắt đầu từ 5
	fmt.Println(add5(2))  // 7 (5 + 2)
	fmt.Println(add5(3))  // 10 (7 + 3)
	fmt.Println(add5(10)) // 20 (10 + 10)

	add10 := adder(10) // Tạo closure mới, bắt đầu từ 10
	fmt.Println(add10(5)) // 15 (10 + 5)
}
```
Đọc xong thì có thể hiểu mỗi closure có bộ nhớ riêng biệt cho biến. Hay khi ta khởi tạo thì closer là riêng biệt chả chung đụng gì cả. Closer này na ná constructer.    
🎯 Tóm tắt  
<ul>Đặc điểm	Closure (func())
<li>Truy cập biến ngoài phạm vi	</li>  
<li>Ghi nhớ giá trị của biến	</li>  
<li>Có thể truyền làm tham số	</li>  
</ul>  
<h1>Recursion</h1>  
Giống y hệt đệ quy trong các ngôn ngữ khác vẫn là stack, định nghĩa case dừng.  
nói chung đệ quy lâu, tốn kém, khó hiểu, bẩn mắt nhiều khi mình đọc solution leetcode còn chả hiểu.  
ví dụ đơn giản trên doc:  

```
func fact(n int) int {
    if n == 0 {
        return 1
    }
    return n * fact(n-1)
}
```

