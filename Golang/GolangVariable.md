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