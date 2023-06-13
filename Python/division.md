"Python division" là phép chia trong ngôn ngữ lập trình Python. Python hỗ trợ hai loại phép chia là phép chia nguyên 
(integer division) và phép chia thực (float division).

Phép chia nguyên (integer division) trong Python được thực hiện bằng toán tử "//".
 Kết quả của phép chia nguyên là một số nguyên, bỏ qua phần dư. Ví dụ:

```python
5 // 2   # kết quả là 2
```

Phép chia thực (float division) trong Python được thực hiện bằng toán tử "/". 
Kết quả của phép chia thực là một số thực. Ví dụ:

```python
5 / 2   # kết quả là 2.5
```

Nếu muốn thực hiện phép chia thực nhưng kết quả là một số nguyên (làm tròn xuống), 
chúng ta có thể sử dụng hàm "floor division" trên module "math":

```python
import math

math.floor(5 / 2)   # kết quả là 2
``` 

Nếu muốn chia hai số và trả về kết quả là một số thực, chúng ta có thể ép kiểu (type casting) một trong hai số thành số thực 
trước khi thực hiện phép chia. Ví dụ:

```python
float(5) / 2   # kết quả là 2.5
5 / float(2)   # kết quả là 2.5
```

Lưu ý rằng trong Python 2, phép chia nguyên và phép chia thực được xử lí khác nhau. Toán tử "/" thực hiện phép chia nguyên, 
trong khi toán tử "//" thực hiện phép chia thực. Tuy nhiên, trong Python 3, toán tử "/" thực hiện phép chia thực, và toán tử "//"
 thực hiện phép chia nguyên.