# Lý thuyết Kafka
* Kafka là nền tảng streaming phân tán, có thể mở rộng và là sản phẩm mã nguồn mở.
* Được viết ra nhằm mục đích cung cấp một nền tảng mà có độ trễ thấp và thông lượng cao cho việc xử lý các nguồn cấp dữ liệu theo thời gian thực.

## Nguyên lý hoạt động
* Dựa trên mô hình Publish/subcrible, tương tự như bất kỳ hệ thống mesage nào khác. Các ứng dụng(đóng vai trò là producer) gửi các messages(bản ghi) tới một node kafka(broker) và nói rằng những messages này sẽ được xử lý bởi các ứng dụng gọi là consumers. Các messages được gửi tới kaffka node sẽ được lưu trữ trong một nơi gọi là topic và sau đó consumer có thể subcrible tới topic đó và lắng nghe những messages này. Messages có thể là bất cứ thông tin gì như giá trị cảm biến, hành động người dùng,...
![alt](https://vsudo.net/blog/wp-content/uploads/2019/12/kien-truc-kafka.jpg)

* Topic có thể được xem như là tên của một danh mục mà các messages sẽ được lưu trữ và đẩy vào.

### Partition
* Không nên lưu trữ tất cả dữ liệu của một topic trên một node, dữ liệu cần được phân chia thành nhiều partition sẽ giúp bảo toàn dữ liệu cũng như xử lý dữ liệu dễ dàng hơn.
* Partitions cho phép chúng ta thực hiện subcribe song song tới một topic cụ thể bằng cách phân chia dữ liệu trong một topic cụ thể bằng cách phân chia dữ liệu trong một topic cụ thể ra cho nhiều broker khác nhau(kafka node), mỗi partition có thể được đặt trên một máy riêng biệt - cho phép nhiều consumer đọc dữ liệu từ một topĩ diễn ra một cách song song.
* Để tăng tính khả dụng(availability) của partition, mỗi partition cũng có giá trị replicas của riêng nó.
![alt](https://vsudo.net/blog/wp-content/uploads/2019/12/partition-kafka.jpg)
* Tất cả các hành động đọc ghi và đọc tới một topic sẽ đều phải đi qua partition leader tương ứng và leader sẽ phối hợp để cập nhật dữ liệu mới tới các replica partition khác. Nếu leader bị hỏng, một trong các replica partition sẽ đảm nhận vai trò là một leader mới.
![alt](https://vsudo.net/blog/wp-content/uploads/2019/12/leader-replica-kafka.jpg)
* Để một producer/consumer ghi/đọc message từ một partition, chắc chắn chúng cần phải biết leader là ai? Kafka lưu trữ những thông tin như vậy là metadata trong một dịch vụ gọi là Zookeeper.

### Cấu trúc dữ liệu log trong Kafka
* Chìa khoá chính dẫn tới khả năng mở rộng và hiệu suất của kafka chính là log (Cấu trúc dữ liệu log)
* Log là một cấu trúc dữ liệu có thứ tự nhất quán mà chỉ hỗ trợ dạng nói thêm(append). Bạn không thểb chỉnh sửa hay xoá các records từ nó. Nó được đọc từ trái sang phải và được đảm bảo thứ tự các item.
![alt](https://vsudo.net/blog/wp-content/uploads/2019/12/log-structure.jpg)
* Một nguồn dữ liệu sẽ được ghi message và log và một hoặc nhiều consumer khác sẽ được message từ log tại thời điểm họ lựa chọn.
* Mỗi entry trong log được định danh bởi một con số gọi là offset, hay nói dễ hiểu offset là giống như chỉ số tuần tự trong một array vậy.
* Vì chuỗi/offset chỉ có thể được duy trì trên từng node/broker cụ thể và không thể duy trì đối với toàn bộ cluster, do đó Kafka chỉ đảm bảo sắp xếp thứ tự dữ liệu cho mỗi partition.

### Parsistence data trong Kafka
* Kafka lưu trữ tất cả message vào disk(không hề lưu trên RAM) và được sắp xếp có thứ tự trong cấu trúc log cho phép kafka tận dụng tối đa khả năng đọc và ghi lên disk một cách tuần tự.
Nó là một cách lựa chọn khá phổ biến để lưu trữ dữ iệu trên disk mà vẫn có thể sử dụng tối đa hoá hiệu năng, 