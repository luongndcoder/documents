## Đặc điểm kiểu dữ liệu
- Hỗ trợ khai báo kiểu dữ liệu động
- Tốc độ biên dịch nhanh
- Hỗ trợ các tác vụ đồng thời
- Ngôn ngữ đơn giản, ngắn gọn

### Đơn giản quá thành ra cũng bỏ đi một số tính năng có trong các ngôn ngữ khác:
- Không hỗ trợ thừa kế
- Không hỗ trợ quá tải toán tử hoặc ghi đè phương thức
- Không hỗ trợ thao tác trên con trỏ (cái này lý do bảo mật nên go ko cho phép)
- Không hỗ trợ kiểu Generic (Hình như từ bản 1.8 là hỗ trợ rồi :D)

## Vào món chính
### Kiểu dữ liệu
- **Interger**: Kiểu số nguyên: unit8 thì nó máy tính phải cung cấp 8 bit cho cái biến được tạo với kiểu dữ liệu đó, tương tự với mấy thằng ở dưới.
    ```text
    KIỂU	GIỚI HẠN
    uint8	0 – 255
    uint16	0 – 65535
    uint32	0 – 4294967295
    uint64	0 – 18446744073709551615
    int8	-128 – 127
    int16	-32768 – 32767
    int32	-2147483648 – 2147483647
    int64	-9223372036854775808 – 9223372036854775807

    Example: var number unit8 = 10
    ```
- **Float**: Kiểu dữ liệu số thực. Đa số sài hai loại dưới để khai báo:
    ```text
    float32
    float64

    Example: var number float = 23.3
    ```
- **String**: Là 1 chuỗi các kí tự bọc trong cặp nháy kép hoặc nháy đơn để biểu diễn văn bản.
    ```text
    string

    Example: var fullname string = "Nguyen Danh Luong"
    ```
- **Boolean**: Chỉ có 1 bit và có 2 giá trị **true** hoặc **false** dịch ra tiếng Việt là hiểu luôn rồi (Yêu em dù true hay false anh đều chấp nhận :D). Có 3 phép toán trong Go thao tác được với giá trị boolean là **&&**(Phép AND), **||** (Phép OR), **!** (Phép NOT).
- Phép AND
    ```text
    BIỂU THỨC	        GIÁ TRỊ
    true && true	    true
    true && false	    false
    false && true	    false
    false && false	    false
    ```
- Phép OR:
    ```text
    BIỂU THỨC	GIÁ TRỊ
    true || true	true
    true || false	true
    false || true	true
    false || false	false
    ```
- Phép NOT:
    ```
    BIỂU THỨC	GIÁ TRỊ
    !true	false
    !false	true
    ```

### Biến 
- Cái này thì ai học qua một ngôn ngữ lập trình rồi thì cũng đã biết hết rồi. Đại ý nó là nơi lưu trữ dữ liệu, một biến gồm có 2 phần là **tên biến** và **kiểu dữ liệu**.
- Các quy tắc tạo ra một biến:
    ```golang
    package main
    
    func main(){
        // Gán thẳng dữ liệu vào biến
        var fullname string = "Hello Luong"
        
        // Hoặc có thể tạo biến rồi gán sau cũng được
        var fullname string
        fullname = "Hello Luong"

        // Go cũng hỗ trợ Dynamic Variable
        first_name := "Luong"

        // Hoặc có thể khai báo nhiều biến trên 1 dòng
        var (first_name, last_name, full_name)
    }
    ```

### Lệnh điều khiển
- Lệnh for:
    ```golang
    package main
    import "fmt"

    var index int = 1
    for index <= 10 {
        fmt.Println(index)
        index = index + 1
    }
    
    // index <= 10: Điều kiện để lặp
    // Hoặc ta cũng có thể viết như này (Giống y chang JS :D)
    for i := 1; i <= 10: i++ {
        fmt.Println(i)
    }
    // Thằng golang này để lặp thì chỉ có mỗi lệnh for này thôi
    // Golang ko support while, do, until, foreach đâu :)))
    ```
- Lệnh if:
    ```golang
    package main
    
    import "fmt"

    func main() {
        for i:= 1; i<= 10; i++ {
            if i % 2 == 0 {
                fmt.Println(i, "chan")
            } else {
                fmt.Println(i, "le")
            }
        }
    }
    // Nếu chia hết cho 2 là chẵn, ngược lại là lẻ (Ez :D)
    // Nó còn in cả index với mỗi lần loop đấy :D
    ```
- Lệnh Switch:
    - **if** xong lại **else if** tầm chục cái cũng chán và nhìn code xấu voãi, thằng này sinh ra để vứt cái **if else** đi cho code đẹp :D.
    ```golang
    package main
    import "fmt"

    func main(){
        switch first_name {
            case "Luong" : fmt.Println("Luong den")
            case "Thai": fmt.Println("Thai dui")
            case "Thien": fmt.Println("Thien cu")
            default: fmt.Println("Thang khac cut x3.14")
        }
    }
    ```
- Các lệnh, biến khác trong Golang:
    - defer: Trì hoãn việc thực thi một hàm cho đến khi hàm xung quanh trả về.
    ```golang
    // Pass a context with a timeout to tell a blocking function that it
	// should abandon its work after the timeout elapses.
    // Việc hủy ngữ cảnh này sẽ giải phóng các tài nguyên được liên kết với nó, vì vậy mã sẽ gọi hủy ngay khi các hoạt động chạy trong Ngữ cảnh này hoàn tất
	ctx, cancel := context.WithTimeout(context.Background(), shortDuration)
	defer cancel()
    ```
    ```env
    MONGO_URI=mongodb://sale:sale123@mongo3.mobio.dev:27017/sale?directConnection=true // Nếu như là 1 cụm cluster
    ```