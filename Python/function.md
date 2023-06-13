Trong Python, một hàm là một khối mã có thể được gọi từ nhiều nơi trong chương trình. 
Hàm có thể nhận đầu vào (các tham số) và trả về một giá trị. Dưới đây là một số kiến thức cơ bản về cách định nghĩa và sử dụng hàm trong Python.

## Định nghĩa hàm

Để định nghĩa một hàm trong Python, chúng ta sử dụng từ khóa "def", theo sau là tên hàm và danh sách các tham số (nếu có).
 Sau đó, chúng ta sử dụng dấu hai chấm để bắt đầu một khối mã mới, cùng với các câu lệnh mà hàm sẽ thực hiện. 
 Cuối cùng, chúng ta sử dụng từ khóa "return" để trả về kết quả.

Cú pháp của định nghĩa hàm như sau:

```python
def <tên_hàm>(<danh_sách_tham_số>):
    <khối_mã>
    return <kết_quả>
```

Ví dụ:

```python
def square(x):
    return x * x
```

Trong ví dụ này, chúng ta định nghĩa một hàm có tên là "square", nhận một tham số là "x". Hàm sẽ trả về giá trị của "x" bình phương.

## Gọi hàm

Sau khi định nghĩa một hàm, chúng ta có thể gọi nó từ bất kỳ đâu trong chương trình bằng cách sử dụng tên của hàm và truyền các tham số tương ứng (nếu có).
Ví dụ:

```python
result = square(5)
print(result)
```

Đầu ra:

```
25
```

Trong ví dụ này, chúng ta gọi hàm "square" với tham số là 5, và lưu kết quả vào biến "result". 
Sau đó, chúng ta in ra giá trị của biến "result".

## Giá trị mặc định của tham số

Trong Python, chúng ta có thể định nghĩa giá trị mặc định cho các tham số của hàm.
 Nếu không có giá trị được truyền cho một tham số, thì giá trị mặc định sẽ được sử dụng. Ví dụ:

```python
def greeting(name, message="Hello"):
    print(message, name)

greeting("Alice")
greeting("Bob", "Hi")
```

Đầu ra:

```
Hello Alice
Hi Bob
```

Trong ví dụ này, chúng ta định nghĩa một hàm có tên là "greeting", nhận hai tham số là "name" và "message".
 Tham số "message" có giá trị mặc định là "Hello". Nếu không có giá trị được truyền cho "message", thì giá trị mặc định sẽ được sử dụng.
  Chúng ta gọi hàm "greeting" hai lần, một lần với một tham số ("Alice") và một lần với hai tham số ("Bob" và "Hi").

## Tham số không xác định trước số lượng

Trong Python, chúng ta có thể định nghĩa một hàm với số lượng tham số không xác định trước. 
Để làm điều này, chúng ta sử dụng ký tự "*" trước tên của tham số. Ví dụ:

```python
def sum(*numbers):
    total = 0
    for number in numbers:
        total += number
    return total

result = sum(1, 2, 3,4, 5)
print(result)
```

Đầu ra:

```
15
```

Trong ví dụ này, chúng ta định nghĩa một hàm có tên là "sum", với một tham số không xác định trước số lượng các tham số được truyền vào (dấu "*numbers").
 Trong thân hàm, chúng ta sử dụng một vòng lặp để tính tổng của tất cả các số được truyền vào. Cuối cùng, chúng ta trả về tổng này. 
 Chúng ta gọi hàm "sum" với năm tham số và in ra kết quả.

## Biến toàn cục và biến cục bộ

Trong Python, có hai loại biến: biến toàn cục và biến cục bộ. 
Biến toàn cục là những biến được định nghĩa bên ngoài các hàm và có thể được sử dụng trong toàn bộ chương trình.
 Biến cục bộ là những biến được định nghĩa bên trong một hàm và chỉ có thể được sử dụng trong phạm vi của hàm đó.

Nếu một biến cục bộ và một biến toàn cục có cùng tên, thì biến cục bộ sẽ được ưu tiên sử dụng trong phạm vi của hàm đó.
 Tuy nhiên, nếu chúng ta muốn truy cập biến toàn cục từ bên trong một hàm, chúng ta có thể sử dụng từ khóa "global". Ví dụ:

```python
x = 10

def f():
    global x
    x = 20
    print(x)

f()
print(x)
```

Đầu ra:

```
20
20
```

Trong ví dụ này, chúng ta định nghĩa một biến toàn cục là "x" với giá trị là 10. Sau đó, chúng ta định nghĩa một hàm "f", 
trong đó chúng ta sử dụng từ khóa "global" để truy cập và thay đổi giá trị của biến toàn cục "x".
 Chúng ta gọi hàm "f" và in ra giá trị của "x" sau khi gọi hàm. Chúng ta thấy rằng giá trị của "x" đã bị thay đổi thành 20,
 cả trong và ngoài hàm "f".