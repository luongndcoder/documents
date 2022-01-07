## Cassandra là gì?
* Là hệ quản trị cơ sở dữ liệu phân tán, thiết kế để xử lý một khối lượng lớn dữ liệu giàn trải trên nhiều node mà vẫn đảm bảo tính sẵn sàng cao(High Availability), khả năng mở rộng hay thu giảm số node linh hoạt(Elastic Scalability) và chấp nhận một số lỗi(Fault Tolerant). Nó được phát triển bằng Facebook.
* Năm 2008 FB chuyển nó cho cộng đồng mà nguồn mở và được Apache phát triển cho tới bh.

### Đặc trưng của Cassandra
* **Tính phân tán và không tập trung(Distributed and dencentralized)**
    * Khả năng phân chia dữ liệu thành nhiều phần, đặt trên nhiều node khác nhau trong khi người dùng vẫn nhận thấy dữ liệu này là một khối thống nhất.
* **Tính mềm dẻo (Elastic scalability)**
    * Hệ thống có thể dễ dàng mở rộng số node trong cluster để có thể phục vụ số lượng lớn request lớn và rút bớt số node khi số lượng request giảm.
* **Tính sẵn sàng cao (High availability)**
    * Dữ liệu được sao lưu thành nhiều bản và được chia hành nhiều node. Điều này mang lại khả năng đáp ứng ngay lập tức cho Cassandra khi client thực hiện tác vụ đọc hay ghi bằng cách thực hiện trên bản sao gần nhất hoặc trên tát cả các bản sao(phụ thuộc vào thông số Consistency Level do Client thiết lập).
* **Tính chấp nhận lỗi (Fault Tolerance)**
    * Do dữ liệu được sao chép thành nhiều bản trên các node của cluster nên kể cả khi dữ liệu ở một node nào đó bị lỗi, bạn vẫn có thể truy xuất dữ liệu của mình trên một node khác.
* **Tuneable consistency**
    * Trong casandra, consistency không phải một hoặc tất cả đề xuất. Vì vậy t có thể giới hạn chính xác hơn đó là **Tuneable consistency** bởi vì khách hàng có thể kiểm soát số lượng bản sao để chặn với tất cả các bản cập nhật. Điều này được thực hiện bằng cách thiết lập các mức độ chống lại nhân tố là các bản sao.
    * **Replication factor** cho bạn quyền quyết định chi phí mà bạn muốn bỏ ra với hiệu năng để tăng thêm tính trong suốt. Bạn thiết lập repication factor để số lượng các node trong cluster mà bạn muốn cập nhật để lan truyền(nhớ răng cập nhật có bao gồm các tác vụ thêm, cập nhật, xoá).
    * **ConsistencyLevel** là thiết lập mà client có thể chỉ rõ ở tất cả các giao dịch và nó cho phép bạn quyết định số lượng bản sao trong cluster được công nhận như là một bản ghi hoạt động hoặc đáp ứng cho việc đọc cđẻ cân nhắc thành công. Đó là một nơi mà Cassandra đưa ra các quyết định cho việc xác định tính thống nhất đến khách hàng.
* **Tính hướng cột(Column oriented key-value store)**
    * Các RDBMS (postgres, mysql) hướng dòng (row-oriented) phải đinh nghĩa trước các cột(column) trong các bảng(table). Đối với Cassandra các bạn không phải làm điều đó, đơn giản là thêm vào bao nhiêu cột cũng được tuỳ theo nhu cầu của bạn
* **Hiệu năng cao(High Performance)**
    * Canssandra được thiết kế riêng biệt từ sơ khai cho đến khi đầy đủ lợi ích cho đa luồng/đa lõi và được chạy trên hàng chục những máy được đặt trong các trung tâm dữ liệu với quy mô nhất quán và liên tục với hàng trăm terabyte dữ liệu. Cassandra đã được chứng minh là hoạt động đặc tốt với yêu cầu tải nặng. Nó luôn có thể hiện thị rất nhanh chóng để ghi mỗi giây trên một máy trạm cơ bản. Khi bạn bổ sung thêm các máy chủ, bạn có thể duy trì tất cả các tính chất mong muốn mà hiệu suất h=không hề bị giảm sút.

## **Giao tiếp Gossip giữa các node trong cassandra** 
* Gossip là một giao thức dùng để cập nhật thông tin về trạng thái của các node khác đang tham gia vào cluster. Đây là một giao thức liên lạc dạng peer-to-peer trong đó mỗi node trao đổi định kỳ thông tin trạng thái của chúng với các node khác mà chúng có liên kết. Tiến trình gossip chạy mỗi giây và trao đổi thông tin với nhiều nhất là ba node khác trong cluster.
Các node trao đổi thông tin về chúng và cả thông tin với các node mà chúng đã trao đổi, bằng cách này toàn bộ những code có thể nhanh chóng hiểu được trạng thái của tất cả các node còn lại trong cluster. Một gói tin gossip bao gồm cả version đi kèm với nó, như thế trong mỗi lần trao đổi gossip, các thông tin cũ sẽ bị ghi đè bởi thông tin mới nhất của một số node.

* Hiểu về cluster membership và seed node.
    * Khi một node được khởi động, nó sẽ xem file cấu hình cassadra.yml để xác định tên cluster chưa nó và các nút khác trong cluster được cáu hình trong file, được biết với tên là seed node.
    * Để ngăn chặn sự đứt đoạn trong truyền thông gossip, tất cả các nút trong cluster phải có 