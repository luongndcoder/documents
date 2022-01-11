## Variable In Python
- Quy tắc đặt tên biến
    - Quy tắc: Tên biến chỉ có thể chứa chữ cái và số gạch dưới _. Có thể bắt đầu bằng chữ cái hoặc dấu gạch dưới, nhưng không được bắt đầu bằng số.
    - _bien, bien nhưng ko đặt 1_bien
    - Khoảng trống (space) không được cho phép khi đặt tên biến, nhưng có thể đặt dấu gạch dưới để tách các từ.
    - Khi đặt tên biến không được sài từ khóa Python và tên hàm.
        - and, del, for, is , raise, asssert, elif, from, lambda, return,
        break, else, global, not, try, class, except, if, or, while, continue, exec, import, pass, yield, def, finally, in, print.
- Các kiểu dữ liệu trong Python
    - có 5 kiểu chuẩn :
        + Number
        + String
        + List
        + Tuple
        + Set
        + Dictionary
    Sài hàm type() để kiểm tra dữ liệu biến
- Number 
    - Hỗ trợ 5 kiểu dữ liệu khác nhau:
        + Int 
        + Float
        + Long
        + Complex(số phức)
        + Fraction
    - Các phép toán cơ bản kiểu number: +,-,/,*,//,**
- String 
    - Thao tác với chuỗi được biểu hiện bằng nhiều cách. Có thể viết dạng dấu nháy đơn ('Luong dep trai') hoặc kép ("Luong dz")(""" Luong funny""") với cùng một kết quả.
    Các chuỗi có thể được lập chỉ mục với số thứ tự trong chuỗi.
     - word = "Python"
     - word[0] => P
     - word[0:2] => "Py"
     - word[2:5] => "tho"

     Nối chuỗi sài toán tử + (vd : "luong" + "dep trai")
- List
    - List được biểu diễn bằng dãy các giá trị, được phân tách bằng dấu phẩy, nằm trong []. Các danh sách có thể chưa nhiều mục có kiểu dữ liệu khác nhau, thông thường là các mục có cùng kiểu (tuy giống array (mảng) cơ mà array thì chỉ chứa các giá trị cùng kiểu dữ liệu thôi, còn list chứa được các giá trị có kiểu dữ liệu khác nhau)
    - VD: list = ["Luong", 21, 8, True]
           arr = [1, 2, 4, 8, 1000]
- Tuple
    -Tuple là một chuỗi các phần tử có thứ tự giống như list. Sự khác biệt giữa list và tuple là chúng ta không thẻ thay đổi các phần tử trong tuple khi đã gán, nhưng trong list thì các phần tử có thể thay đổi. Tuple thường được sử dụng cho các dữ liệu không cho phép sửa đổi.
    - Tuple thường được sử dụng cho các phần tử không cùng kiểu dữ liệu và list thường sử dụng cho các phần tử có cùng kiểu dử liệu. Việc tuple không thay đổi khi sử dụng nên khi sử dụng sẽ đảm bảo các dữ liệu đó không bị thay đổi
    - Tuple được tạo bằng cách đặt tất cả các phần tử của nó trong dấu ngoặc đơn(),
    phân tách bằng dấu phẩy. (nói chung viết dấu ngoặc đơn vào cho tường minh code đã khó đọc rồi còn chơi xoắn thì chịu )
    - Không bị giới hạn phần tử và có thể có nhiều kiểu dử líệu khác nhau(int, float, str, list...)
    - Tạo tuple có một phần tử thì nhớ là cần thêm dấu phẩy nữa nhé, không là không biết nó là kiểu dữ liệu gì đâu (VD: my_tuple = ("Luong",)) có cái dấu phẩy không lỗi đâu.
    - Truy cập phần tử trong tuple cũng giống list ta sài cái này []:
        my_profile = ("Luong", 21, [20, 8, 2000])
        print("birthday", my_profile[2: 2]) // 2000 
    - Tuple không thể thay đổi, cũng không thể xóa một phần tử nào của nó một khi được tạo ra, nhưng nếu bản thân một phần tử trong kiểu này là kiểu dữ liệu có thể thay đổi thì ta vẫn có thể thay đổi giá trị của phần tử đó trong Tuple.
    - VD: my_profile = ("Luong", 21, [20, 8, 2000])
          my_profile[1] = 18 // lỗi mọe luôn 
          my_profile[2][2] = 2002 // gút chóp luôn 
    - Muốn xóa một tuple thì chỉ cần sài : del my_profile ( là bay màu ngay :v)
