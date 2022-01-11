# Những giá trị mặc định trong Kafka bạn nên quan tâm
![alt](https://vsudo.net/blog/wp-content/uploads/2020/01/gia-tri-mac-dinh-kafka-1295x420.jpg)
* Có rất nhiều thông số cấu hình mặc định có sẵn trong Apache Kafka, hầu hết những giá trị này có thể tuỳ chỉnh được - giúp tinh chỉnh sản phẩm nhằm đáp ứng những yêu cầu phù hợp cho hệ thống(độ trễ, thoughtput, performance, ...). Những giá trị mặc định này trải dài trên nhiều thành phần khác nhau như: broker, producer và consumer.

* Thường thì Kafka cung cấp càng nhiều thông số cấu hình, sẽ giúp chúng ta tuỳ chỉnh hệ thống một cách toàn diện hơn, nhưng một số thông số cấu hình trong đó có thể trở nên tương đối nguy hiểm nếu chúng được sử dụng sai cách. Vì chúng có thể có những tác dụng phụ không mong muốn, hay được tối ưu hoá cho một số mục đích nào đó mà không dành cho bạn.

## Những giá trị mặc định bạn nên thay đổi
### 1. auto.create.topics.enable
* Mặc định giá trị này được thiết lập "true". Bạn sẽ muốn thay đổi giá trị này thành **false**. Vì các ứng dụng thường sẽ phải chịu trách nhiệm cho việc tạo ra các topics của chúng.

* Nếu bạn để giá trị này là true, một số thông số cấu hình khác sẽ được kích hoạt để đáp ứng cấu hình này cho topic.

* log.retention.hours: mặc định, logs sẽ được giữ lại 7 ngày. Bất kỳ dữ liệu nào được lưu trữ quá 7 ngày sẽ không được giữ lại nữa.

* min.insync.replicas: mặc định giá trị này là 1. Như theo documentation Kafka có đề cập đến, giá trị cấu hình này điển hình sẽ là replication-factor từ đi 1, nghĩa là nếu replication-factor bạn thiết lập giá trị là 3