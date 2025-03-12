**Array**  

syntax declaration: `var a [3]int`  
method `len()` to get length of array.

các cách khai báo khác:  
shorthand: `b := [5]int{1, 2, 3, 4, 5}`  

không biết trước độ dài mảng: ` b := [...]int{1, 2, 3, 4, 5}`  

Chỉ định cụ thể phần tử, các phần tử ở giữa sẽ bị gán = 0
If you specify the index with :, the elements in between will be zeroed.  
`b = [...]int{100, 3: 400, 500}`  
Output  
```[100 0 0 400 500]```  

Mảng nhiều chiều:  
```
var twoD [2][3]int
twoD = [2][3]int{
        {1, 2, 3},
        {1, 2, 3},
    }
```

**Slice**

Slice là 1 kiểu dữ liệu quan trọng trong Go, mạnh mẽ với 1 interface cho sequences hơn array.

Đọc xong mình không thấy khác array mấy, có vẻ đây giống như vector trong C++. size không cố định. 
Để sử dụng cần import package `"slice"`  
`null` trong Go có vẻ được ghi là `nil`  
Khởi tạo 1 slice:
`var s []string`
như này thì `s == nil` và len sẽ = 0  
muốn cấp phát kích sẵn cho nó mà không muốn nó là null thì dùng `make`  
` s = make([]string, 3)` giờ đây len(s) = 3 và cap(s) = 3
cap là sức chứa của slice, khi thực hiện lệnh make có khai báo cap, dòng make ở trên chưa có![Uploading slice-1.png…]()
 nên mặc định cap = len = 3. `s = make([]string, 3,4)`  
Như này thì cap của s là 4 tức là khi `append` phần tử mới vào nó không cần cấp phát bộ nhớ do mình đã xin rồi. Nếu append quá cap thì xin Go tự xin cấp phát lại và cap *=2.

có thể dùng kiểu `slice[low:high]` y như python để lấy phần tử từ low đến high-1  
**Slice Internal** 
![image](https://github.com/user-attachments/assets/0f8a6b55-328f-4bac-859b-cbc4267ff054)  
Array đơn giản chỉ là 1 chuỗi các phần tử, ví dụ arr [4]int thì trong bộ nhớ là 4 biến int cạnh nhau.  
Nhưng với slice thì nó như hình ảnh gồm có pointer đến array, len của slice và cap của slice. Đến đây có thể hiểu hàm `make`  
![image](https://github.com/user-attachments/assets/c36b6414-fff3-4c0e-a1ff-a5f1c397ef05)  

Trong example người ta không chỉ ra nhưng có dùng hàm copy: 
```
 c := make([]string, len(s))
    copy(c, s)
```
mình không biết liệu pointer ở c vẫn trỏ vào arr mà pointer ở s trỏ vào hay tạo ra mảng mới riêng để trỏ. Hỏi gpt thì nó bảo là trỏ đến mảng mới.  
Thử tạo 1 slice mới bằng lệnh copy từ s và thử đổi `c[0]` thì thấy không ảnh hưởng đến s.
```
cpy: [0 0 0 5]
cpy: [1 0 0 5]
s: [0 0 0 5]
```


