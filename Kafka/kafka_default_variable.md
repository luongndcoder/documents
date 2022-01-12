# Những giá trị mặc định trong Kafka bạn nên quan tâm
![alt](https://vsudo.net/blog/wp-content/uploads/2020/01/gia-tri-mac-dinh-kafka-1295x420.jpg)
* Có rất nhiều thông số cấu hình mặc định có sẵn trong Apache Kafka, hầu hết những giá trị này có thể tuỳ chỉnh được - giúp tinh chỉnh sản phẩm nhằm đáp ứng những yêu cầu phù hợp cho hệ thống(độ trễ, thoughtput, performance, ...). Những giá trị mặc định này trải dài trên nhiều thành phần khác nhau như: broker, producer và consumer.

* Thường thì Kafka cung cấp càng nhiều thông số cấu hình, sẽ giúp chúng ta tuỳ chỉnh hệ thống một cách toàn diện hơn, nhưng một số thông số cấu hình trong đó có thể trở nên tương đối nguy hiểm nếu chúng được sử dụng sai cách. Vì chúng có thể có những tác dụng phụ không mong muốn, hay được tối ưu hoá cho một số mục đích nào đó mà không dành cho bạn.

## Những giá trị mặc định bạn nên thay đổi
### 1. auto.create.topics.enable
* Mặc định giá trị này được thiết lập "true". Bạn sẽ muốn thay đổi giá trị này thành **false**. Vì các ứng dụng thường sẽ phải chịu trách nhiệm cho việc tạo ra các topics của chúng.

* Nếu bạn để giá trị này là true, một số thông số cấu hình khác sẽ được kích hoạt để đáp ứng cấu hình này cho topic.

* **log.retention.hours**: mặc định, logs sẽ được giữ lại 7 ngày. Bất kỳ dữ liệu nào được lưu trữ quá 7 ngày sẽ không được giữ lại nữa.

* **min.insync.replicas**: mặc định giá trị này là 1. Như theo documentation Kafka có đề cập đến, giá trị cấu hình này điển hình sẽ là **replication-factor** từ đi 1, nghĩa là nếu **replication-factor** bạn thiết lập giá trị là 3, khi đó **min.insync.replicas** nên là 2. Vấn đề khi bạn sử dụng giá trị mặc định là 1, nghĩa là bạn đang đặt mình vào trạng thái nguy hiểm - trong đó cluster chấp nhận vác message khi mà bạn chỉ có 1 bản copy. Mặt khác, giá trị này bằng với replication-factor (yếu tố nhân rộng) nghĩa là bạn sẽ mất đi 1 node broker tạm thời mà không nhận thêm được message nào nữa cho đến khi missing partition(phân vùng bị thiếu) được rebalanced(cân bằng) lại để trở thành headlthy node(nút đầu).
* **default.replication.factor**: mặc định giá trị này là 1. Giá trị mặc định như vậy hơi bị dở, vì nó thực sự chỉ tạo ra 1 bản copy của một topic một cách tự động. Nếu disk lưu trữ partition của topic này chết, khi đó dữ liệu sẽ hoàn toàn bị mất. Thậm chí nếu như bạn có backup, consumer sẽ vẫn gặp trục trặc khi rebalance tới broker khác mà có bản copy của partition, dẫn đến việc consumer lấy message sẽ bị ngắt đoạn. Thiết lập giá trị bằng 3 sẽ là con số hợp lý.
* **num.partitions**: mặc định là 1. Giá trị mặc định này cũng không tốt. Nếu một topic chỉ có một partition, nó có thể được sử dụng chỉ bởi một instance của một ứng dụng tại một thời điểm cụ thể, dẫn đến việc cản trở quá trình nhận dữ liệu song song khi sử dụng Kafka. Mặc dù Kafka cluster có giới hạn về số lượng chúng có thể xử lý, gía trị tối thiểu 3 partition mỗi topic thường sẽ an toàn và hợp lý hơn.

* **offsets.retention.minutes**:
    * Mặc định là 1400 phút(24 giờ). Giá trị mặc định này khá là nguy hiểm. Một số ứng dụng có thể rơi vào trạng thái nghỉ vào thời gian cuối tuần, nghĩa là chúng không đẩy message nào tới Kafka trong khoảng thời gian đó.

    * Buổi sáng này hôm sau, nếu chúng khởi động lại trước khi consumer từ Kafka, instance mới không thể tìm thấy bất kỳ **commited offsets** nào cho consumer group, vì chúng đã hết hạn.

    * Do đó, cấu hình auto.offset.reset trong consumer khởi động, gửi ứng dụng tới các message cũ nhất, mới nhất hoặc không thành công. Trong bất kỳ trường hợp nào đi nữa, điều này cũng không nên.


