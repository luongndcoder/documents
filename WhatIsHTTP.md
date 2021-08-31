# What is HTTP?
- HTTP (HyperText Transfer Protocol) là gì?  
    - ( Là giao thức truyền tải siêu văn bản ) Là một giao thức lớp ứng dụng cho các hệ thống thông tin siêu phương tiện phân tán, cộng tác.
- Khía cạnh cơ bản của HTTP
    -  HTTP đơn giản
        - Thường được thiết kế để trở nên đơn giản và thân thiện để con con người có thể đọc được, ngay cả khi có thêm sự phức tạp được giới thiệu trong HTTP/2 bằng cách đóng gói các HTTP message thành các frame. Với các HTTP message, chúng ta có thể được đọc và hiểu được, cung cấp khả năng testing hơn cho các dev và giảm thiểu độ phức tạp cho bất cứ người mới nào.
    - HTTP có thể mở rộng
    - HTTP là stateless, nhưng không sessionless
        - Không có liên kết giữa 2 yêu cầu được thực hiện liên tếp trên cùng 1 kết nối.
    - Cấu trúc cơ bản của HTTP (ảnh nguồn TopDev)
        ![](https://topdev.vn/blog/wp-content/uploads/2020/10/http-la-gi-1.gif)
        - HTTP còn là một giao thức **Yêu Cầu** - **Phản hồi** dựa trên cấu trúc Client - Server
    - Kết nối của HTTP
        - HTTP dựa trên tiêu chuẩn TCP vốn là connection-based(dựa trên sự kết nối).
        - Trước khi 1 Client(Điện thoại, Máy tính, ...) có thể trao đổi 1 cặp yêu cầu - phản hồi HTTP, chúng phải thiết lập 1 kết nối TCP, 1 quá trình vốn yêu cầu - phản hồi HTTP. Điều này làm nó kém hiệu quả hiwn việc chia sẻ 1 kết nối TCP đơn lẻ khi nhiều yêu cầu được gửi liên tiếp.