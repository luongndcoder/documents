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
Nó là một cách lựa chọn khá phổ biến để lưu trữ dữ iệu trên disk mà vẫn có thể sử dụng tối đa hoá hiệu năng, có một số lý do chính dưới đây:
    * Kafka có một giao thức mà nhóm các message lại với nhau. Điều này cho phép các request network nhóm các message lại với nhau, giúp giảm thiểu chi phí sử dụng tài nguyên mạng, giúp giảm thiểu chi phí sử dụng tài nguyên mạng, server, gom các message lại thành một cục và consumer sẽ tìm nạp một khối messsage cùng một lúc - do đó sẽ giảm tải disk cho hệ điều hành.
    * Kafka phụ thuộc khá nhiều và pagecache của hệ điều hành cho việc lưu trữ dữ liệu, sử dụng RAM trên máy một cách hiệu quả.
    * Kafka lưu trữ các messages dưới định dạng nhị phân xuyên suốt quá trình (producer > broker > consumer), làm cho nó có thể tận dụng tối ưu hoá khả năng zero-copy. Nghĩ là khi hệ điều hành copy dữ liệu từ pagecahce trực tiếp sang socket, hoàn toàn bỏ qua ứng dụng trung gian là kafka.
    * Đọc/ghi dữ liệu tuyến tính trên disk nhanh. Vấn đề làm cho disk chậm hiện nay thường là do quá trình tìm kiếm trên disk nhiều lần. Kafka đọc và ghi trên disk tuyến tính, do đó nó có thể tận dụng tối đá hoá hiệu suất trên disk.
### Consumer và Consumer Group 
* Consumer đọc các messages từ bất kỳ partition nào, cho phép bạn mở rộng lượng message được sử dụng tương tự như cách các producer cung cấp message.
* Consumer cũng được tổ chức thành các consumer groups cho một topic cụ thể - mỗi consumer bên trong group đọc message từ một partition duy nhất, để trách việc 2 consumer xử lý đọc cùng một message 2 lần và toàn bộ group xử lý tất cả các message từ toàn bộ topic.
    * Nếu bạn có số consumer > số partition, khi đó một số consumer sẽ ở chế độ rảnh rỗi bởi vì chúng không có partition nào để xử lý.
    * Nếu bạn có số partition > số consumer, khi đó consumer sẽ nhận các message từ nhiều partition.
    * Nếu bạn có số partition = số partition, mỗi consumer sẽ đọc message theo thứ tự 1 partition.
* Xem qua hình ảnh bên dưới:
![alt](https://vsudo.net/blog/wp-content/uploads/2019/12/group-consumer.jpg)

* Kafka tuân thủ theo quy tắc được cung cấp bởi broker và consumer. Nghĩa là kafka không theo dõi các record được đọc bởi consumer và do đó không biết gì về hành vi của consumer. Việc giữ lại các messages trong một khoảng thời gian được cấu hình trước và nó tuỳ thuộc vào consumer, để điều chỉnh thời gian sao cho phù hợp. Bản thân consumer sẽ thăm dò xem Kafka có message nào mới hay không và cho kafka biết những record nào chúng muốn đọc. Điều này cho phép chúng tăng/ giảm offset mà consumer muốn, do đó nó có thể đọc lại các message đã được đọc rồi và tái xử lý các sự kiện trong trường hợp gặp sự cố.
* Ví dụ: Nếu Kafka được cấu hình để giữ lại các messages tồn tại trong một ngày và consumer bị down lâu hơn 1 ngày, khi đó consumer sẽ mất message. Tuy nhiên, nếu consumer chỉ bị down trong khoảng 1 giờ đồng hồ, khi đó nó hoàn toàn có thể bắt đầu đọc lại message từ offset mới nhất.

### Vai trò của Zookeeper
* Zookeeper đóng vai trò là nơi lưu trữ dữ liệu phân tán dạng key-value. Nó được tối ưu hoá cho tác vụ đọc nhanh nhưng ghi chậm. Kafka sử dụng Zookeeper cũng được thiết kế cho khả năng chịu lỗi cao, do đó Kafka phụ thuộc khá nhiều vào Zookeeper. 
* Nó cũng được sử dụng để lưu trữ tất cả metadata như là:
    * Offset cho mỗi partiotion của consumer group 
    * ACL (Access control list) - được sử dụng cho việc giới hạn truy cập/ uỷ quyền.
    * Quota của consumer/producer - số lượng messsage tối đa mỗi giây
    * Partition Leader và trạng thái của chúng

* Producer và consumer không tương tác trực tiếp với Zookeeper để biết leader của partition hay những metadata khác, thay vào đó chúng sẽ truy vấn metadata tới Kafka broker - sau đó Kafka tương tác với Zookeeper và gửi phản hồi metadata về lại cho chúng.

### Kết luận
Kafka cho phép có một lượng clowns các messages đi qua một phương tiện tập trung và lưu trữ chúng mà không cần phải lo lắng gì về những vấn đề như hiệu suất hay mất mát dữ liệu. Kafka có thể là thành phân trung tâm trong mô hình kiến trúc hướng sự kiện (event-driven) và cho phép bạn phân tách giữa ứng dụng này với ứng dụng khác.

## Các câu hỏi thường gặp
* Kafka có khả năng gì?
    * Thể hiện 3 khả năng chính như sau:
        * Cơ chế publish/subcribe tương tự như các hệ thống message queue doanh nghiệp khác.
        * Cơ chế lưu trữ stream các bản ghi trên nhiều node broker khác nhau, giúp khắc phục lỗi xảy ra.
        * Xử lý stream các bản ghi ngay khi nó vừa đến.
* Các thành phần chính trong Kafka là gì?
    * Có 4 thành phần khác nhau như sau:
        * Kafka Broker
        * Zookeeper
        * Producer
        * Consumer
* Mục đích chính khi sử dụng Apache Kafka là gì?
    * Sử dụng để theo dõi lưu lượng truy cập, giám sát web server.
    * Xử lý sự kiện
