## Blockchain Learning Path
# Pre-requisites
    - Public key cryptography (mật mã khóa công khai)
        + Là phương pháp mã hóa dữ liệu bằng hai khóa khác nhau và làm cho một trong các khóa, khóa công khai (public key) có sẵn cho mọi người sử dụng. Khóa còn lại gọi là khóa cá nhân (private key). Dữ liệu được mã hóa bằng khóa công khai chỉ có thể được giải mã bằng khóa riêng tư và dữ liệu của khóa riêng tư chỉ có thể được giải mã bằng khóa công khai.
        + Mã hóa khóa công khai còn được gọi là mã hóa không đối xứng.
        + Cách thức hoạt động có thể xem thêm [ở đây](https://www.cloudflare.com/learning/ssl/how-does-public-key-encryption-work/)
    - Digital signatures (Mật mã chữ ký điện tử)
        + Là khóa công khai ban đầu của xác thực thông điệp.
        + Là một kỹ thuật liên kết một người/ thực thể với dữ liệu kỹ thuật số. Ràng buộc này có thể được xác nhận đọc lâọ bởi người nhận cũng như bất kỳ bên thứ ba nào.
        => Là một giá trị mật mã được tính toán từ dữ liệu và một khóa bí mật chỉ người ký mới biết.
        (Mô hình chữ ký số)![](https://www.tutorialspoint.com/cryptography/images/model_digital_signature.jpg)
        + Thông tin thêm : 
        ![Mô hình chữ ký số](https://www.tutorialspoint.com/cryptography/cryptography_digital_signatures.htm)

    - Cryptographic hashing:
        + Hashing on the Blockchain:
            + Băm có nghĩa là lấy đầu vào có độ dài bất kỳ và trả lại đầu ra có độ dài cố định
            + Các thuật toán băm phổ biến như 256, sha256
            + Trong sha256 dù đầu vào lớn hay nhỏ thì đầu ra sẽ luôn có độ dài 256 bit cố định, điều này rất quan trong khi xử lý một lượng lớn dữ liệu và giao dịch. Thay vì ghi nhớ một lượng lớn dữ liệu  bạn có thể nhớ hàm băm để theo dõi một hàm băm mật mã là một loại hàm băm đặc biệt.
            + Cryptographic Hash Function (Hàm băm đặc biệt):
                - Gồm 6 thuộc tính :
                1. Deterministic (Xác định)
                    - Nhập cùng một dữ liệu thì sẽ luôn nhận về một kết quả.
                2. Quick Computation (Tính toán nhanh)
                3. Pre-Image Resistance
                4. A Small Change in Input Changes the Output 
                5. Collision Resistant
                6. Puzzle Friendly
# Blockchain
    - Blockchain là một loại cơ sở dữ liệu cụ thể.
    - Nó khác với một cơ sở dữ liệu điển hình ở cách nó lưu trữ thông tin. Các blockchians lưu trữ dữ liệu trong các khối sau đó được liên kết với nhau.
    - Khi dữ liệu mới đến, nó được nhập vào một khối mới. Khi khối chưa đầy dữ liệu, nó sẽ được xâu chuỗi vào khối trước đó, điều này làm cho dữ liệu được liên kết với nhau theo thứ tự thời gian.
    - Các loại thông tin khác nhau có thể được lưu trữ trên một blockchain nhưng cách sử dụng phổ biến nhất cho đến nay là làm sổ cái cho các giao duchj,
    - Trong trường hợp bitcoin, blockchian được sử dụng theo cách phi tập trung để không một các nhân hoặc nhóm nào có quyền kiểm soát - thay vào đó, tất cả người dùng đều giữ quyền kiểm soát chung.
    - Các blockchains phi tập trung là bất biến, có nghĩa là dữ liệu đã nhâp là không thể thay đổi. Đối với Bitcoin, điều này có nghĩa là các giao dịch được ghi lại vĩnh viễn và bất kỳ ai cũng có thể xem được.

    + Cấu trúc lưu trữ :
        - Một điểm khác biệt chính giữ CSDL điển hình và blockchain là cách dữ liệu được cấu trúc. Một chuỗi khối thu thập thông tin với nhau theo các nhóm còn được gọi là các khối, chứa các tập hợp thông tin. Các khối có khả năng lưu trữ nhất định và khi được lấp đầy, sẽ được liên kết với khối đã được lấp đầy trước đó, tạo thành một chuỗi dữ liệu gọi là "blockchain". Tất cả thông tin mới theo sau khối mới thêm đó được biên dịch thành một khối mới được hình thành, sau đó cũng sẽ được thêm vào chuỗi sau khi được lấp đầy.
        - Cơ sở dữ liệu cấu trúc dữ liệu của nó thành các bảng trong khi blockchain, giống như tên gọi của nó, cấu trúc dữ liệu của nó thành thành các phần (khối) được liên kết với nhau. Điều này làm cho tất cả các blockchains đều là cơ sở dữ liệu nhưng không phải tất cả các cơ sở dữ liệu đều là blockchains. Hệ thống này cũng tạo ra một dòng thời gian không thể thay đổi của dữ liệu khi được thực hiện theo bản chất phi tập trung. Khi một khối được lấp đầy, nó sẽ được đặt trong đá và trở thành một phần của dòng thời gian này. Một khối trong chuỗi được cung cấp một dấu thời gian chính xác khi nó được thêm vào chuỗi.

    + Quy trình giao dịch: ("Nguồn investopedia")![](https://www.investopedia.com/thmb/OspmuCTSRyVEcNwSLOwYGaQHm64=/1688x0/filters:no_upscale():max_bytes(150000):strip_icc():format(webp)/dotdash_Final_Blockchain_Sep_2020-01-60f31a638c4944abbcfde92e1a408a30.jpg)
        - Một giao dịch mới được nhập
        - Giao dịch sau đó được truyền tới một mạng lưới các máy tính ngang hàng nằm rải rác trên thế giới.
        - Mạng máy tính sau đó giải các phương trình để xác nhận tính hợp lệ của giao dịch
        - Sau khi được xác nhận là các giao dịch hợp pháp, chúng được nhóm lại với nhau thành các khối
        - Các khối này sau đó được liên kết với nhau tạo ra một lịch sử lâu dài của tất cả các giao dịch là vĩnh viễn.
        - Giao dịch hoàn thành .

    + Các thuộc tính của tiền điện tử: ("Nguồn investopedia") ("Nguồn investopedia")![](https://www.investopedia.com/thmb/l3UhugQHQsDGfoOYFE3jOiIgCNA=/5855x0/filters:no_upscale():max_bytes(150000):strip_icc():format(webp)/dotdash_Final_Blockchain_Sep_2020-02-d8258ab814a34756bf51f1f95c78dc63.jpg)
        - Trong khi blockchain chủ yếu sử dụng để lưu trữ lịch sử giao dịch tiền điện tử, những thứ khác như hợp đồng pháp lý, kiểm kê sản phẩm có thể được lưu trữ.
        - Có giá trị nội tại vì nó là một cách bảo mật đáng tin cậy và cách nhanh chóng để chuyển giá trị cho với chi phí thấp hoặc miễn phí.
        - Không có ở dạng vật lý(ngoài đời) vì nó chỉ tồn tại trên blockchain bất biến.
        - Các thuộc tính của tiền điện tử như tổng nguồn cung của nó được quyết định bởi phần lớn các thành viên trong mạng lưới phi tập trung của nó thay vì ngân hàng trung ương.
    + Phân quyền :
        - Giống như một CSDL, Bitcoin cần một tập hợp các máy tính để lưu trữ chuỗi khối của nó. Đối với bitcoin, blockchain này chỉ là một loại cơ sở dữ liệu cụ thể lưu trữ mọi giao dịch Bitcoin từng được thực hiện.
        - Bitcoin bao gồm hàng nghìn máy tính, nhưng mỗi máy tính hoặc nhóm máy tính chưa blockchain của nó lại ở một vị trí địa lý khác nhau và chúng đều được vận hành bởi các cá nhân hoặc nhóm người riêng biệt. Những máy tính tạo nên mạng của Bitcoin được gọi là các nút.(nodes)
        - Trong một blockchain, mỗi nút có một bản ghi đầy đủ về dữ liệu đã được lưu trữ trên blockchain kể từ khi thành lập. Đối với bitcoin, dữ là toàn bộ lịch sử của tất cả giao dịch Bitcoin. Nếu một nút có lỗi trong dữ liệu của nó , nó có thể sử dụng hàng nghìn nút khác làm điểm tham chiếu để chỉnh sửa nó. Bằng cách này, không một nút nào có thể thay đổi được thông tin được lưu trữ bên trong nó.Do đó lịch sử của các giao dịch trong mỗi khối tạo nên chuỗi khối của Bitcoin là không thể thay đổi.
    + Minh bạch 
        - Do tính chất phi tập trung của chỗi khối Bitcoin, tất cả các giao dịch có thể được xem một cách minh bạch bằng cách có một nút cá nhân hoặc bằng cách sử dụng các trình khám phá chuỗi khớp cho phép bất kỳ ai cũng có thể xem các giao dịch đang diễn ra trực tiếp. Mỗi nút có bản sao của chuỗi riêng của nó được cập nhật khi các khối mới được xác nhận và thêm vào. Điều này có nghĩa là nếu bạn muốn, bạn có thể theo dõi Bitcoin ở bất cứ đâu.
    - Blockchain có an toàn không ?

    - Bitcoin so với Blockchain
        - Bitcoin chỉ đơn thuần sử dụng blockchain như một phương tiện để ghi lại sổ cái thanh toán một cách minh bạch, nhưng về lý thuyết, blockchain có thể được sử dụng để ghi lại bất kỳ số lượng điểm dữ liệu nào. Như đã thỏa thuận, điều này có thể ở dạng giao dịch, phiếu bầu trong một cuộc bầu cử, kiểm kê sản phẩm, danh tính tiểu bang, giấy chứng nhận nhà,...
    
    - Blockchain vs Banks
    
    - Ưu và nhược điểm của Blockchain
        - Ưu điểm :
            + Cải thiện độ chính xác bằng cách loại bỏ sự tham gia của con người vào quá trình xác minh
            + Giảm chi phí bằng cách loại bỏ xác minh bên thứ ba
            + Phi tập trung làm cho việc giả mạo trở nên khó hơn
            + Giao dịch an toàn, riêng tư và hiệu quả
            + Công nghệ minh bạch
            + Cung cấp giải pháp thay thế ngân hàng và cách để bảo mật thông tin cá nhân cho các công dân của các quốc gia có chính phủ không ổn định hoặc kém phát triển.

        - Nhược điểm: 
            + Chi phí công nghệ đáng kể liên quan đến khai thác bitcoin
            + Giao dịch thấp mỗi giây
            + Lịch sử sử dụng trong các hoạt động bất hợp pháp
            + Quy định
        