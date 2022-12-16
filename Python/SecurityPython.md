## Security trong Python
- Python là một ngôn ngữ thông dịch nên không cần build để chạy, nó được biên dịch mã byte, rất khó để khoá. Tuy nhiên Cython ra đời giúp cho code Python được compaine ra file build giúp cho các nhà phát triển ứng dụng bằng code Python được bảo mật code khi đưa ứng dụng của mình đến các hệ thống on premise của khách không bị copy code hoặc sửa chữa code của hệ thống.
- Sẽ có các hợp đồng, điều khoản không cho phép làm việc đó tuy nhiên việc chặn trên giấy tờ không thể phủ được hết các case (vì máy của khách thì họ vào lúc nào chả được :D) nên việc bảo mật code là lựa chọn tốt nhất để không bị mất code.

# Sơ qua về Cython (Cái cần để mã hoá code Python của bạn)
- Theo định nghĩa từ infoworld,  "Cython is a superset of Python that compiles to C, Cython combines the ease of Python and the speed of native code". Tạm dịch Cython là một thay thế của python có thể biên dịch thành C, Cython kết hợp sự đơn giản của Python và tốc độ của C. Cơ mà đây là dùng Cython để mã hoá nên việc tăng tốc độ của Python là không có nhé :D, kết quả là bằng nhau. Chỉ khi bạn code theo cú pháp của Cython file **.pyx** và với các hàm, kiểu dữ liệu của Cython thì lúc đó hiêụ năng với đúng như lời đồn nhé.

# Vào món chính (Cách build Cython để mã hoá Python)
- Mình sẽ lấy một ví dụ mà đa số ae code Python từ cấp Mẫu giáo đến cấp Đại học đều đã nghe qua là **Flask** để thực hiện Example cũng như kiểm tra hiệu năng.
- Warning: Các phần thực hành được run trên OS Macos nên có thể các ae sài Window có thể phải điều chỉnh vài câu lệnh trên Terminal của mình để cho nó work, cơ mà không nhiều đâu (nhiều thì cài Ubuntu hoặc mua Mac code dùng Linux code sướng lắm :D)

- Đầu tiên: Kiểm tra xem máy mình cài python chưa nhé, chưa cài thì khỏi đọc bước tiếp theo luôn cũng được :D.

B1: Open terminal (Power Shell trên Window):
    + Vào thư mục mà bạn muốn lưu cái Project mà bạn đang muốn thực hiện: **cd /Documents/learn-python/**
    + Tạo project vào môi trường ảo gõ: **mkdir PythonSecurity && cd PythonSecurity && python3.8 -m venv venv && source venv/bin/active**
    + Sài VS Code thì chỉ cần gõ: **code .** là nó open cái Project của bạn bằng VS code.
    + Giờ tạo một file lưu trữ các lib versions pip của project thôi: Trên project tạo một file **requirements.txt**
    + Truy cập vào file requirements.txt thêm các lib cần thiết (**Nhớ bỏ cái dấu + đầu dòng đi đấy, copy vào nữa thì ko đỡ được**): 
        + Cython == 0.29.32
        + Flask == 2.2.2
    + Ok roài, giờ bật cái terminal lên (Nhớ phải active môi trường nhé) gõ: pip install -r requirements.txt
    + Cài mà thấy nó ko có gì màu đỏ là cài xong rồi đấy (còn nó mà có cái màu vàng thì kệ nó)
    + Giờ tạo một file setup.py có thông tin sau:
        - 