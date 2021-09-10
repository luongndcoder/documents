## Blockchain Ethereum
- Về cơ bản là một máy trạng thái dựa trên giao dịch.
- Trong khoa học máy tính, máy trạng thái đề cập đến một thứ gì đó sẽ đọc một loạt đầu vào dựa trên những đầu vào đó, sẽ chuyển sang trạng thái mới.
- Với máy trạng thái của Ethereum, chúng tôi bắt đầu với " genesis state " (trạng thái khởi đầu). Điều này tương tự như một phương tiện chặn trống, trước khi bất kỳ giao dịch nào xảy ra trên mạng. Khi các giao dịch được thực hiện, trạng thái ban đầu này sẽ chuyển sang trạng thái cuối cùng. Tại bất kỳ thời điểm nào, trạng thái cuối cùng này đại diện cho trạng thái hiện tại của Ethereum.
- Trạng thái của Ethereum có hàng triệu giao dịch. Các giao dịch này được nhóm thành "block". Một block chứa một loạt các giao dịch và mỗi block được liên kết với nhau với khối trước đó.

- Để một giao dịch được coi là hợp lệ, nó phải trải qua một quá trình xác nhận được gọi là khai thác. Khai thác là khi một nhóm các nodes(tức là máy tính) sử dụng tài nguyên máy tính của họ để tạo ra một khối giao dịch hợp lệ.
- bất kỳ nút nào trên mạng tự tuyên bố là người khai thác đều có thể cố gắng tạo và xác thực một khối. Rất nhiều thợ mỏ từ khắp nơi trên thế giới cố gắng tạo và xác thực các khối cùng một lúc.
- Để một khối được thêm vào blockchain chính, người khai thác phải chứng minh nó nhanh hơn bất kỳ người khai thác nào khác của đối thủ cạnh tranh. Quá trình xác nhận từng khối bằng cách yêu cầu người khai thác cung cấp một bằng chứng toán học được gọi là "Bằng chứng công việc".
- Người khai thác nhận một khối mới sẽ được thưởng một lượng giá trị nhất định khi thực hiện công việc này. Giá trị đó là: Chuỗi khối Ethereum sử dụng một mã thông báo kỹ thuật số nội tại được gọi là “Ether”. Mỗi khi người khai thác chứng minh được một khối, các mã thông báo Ether mới sẽ được tạo và trao thưởng.
+ Điều gì đảm bảo rằng mọi người đều dính vào một chuỗi khối? Làm thế nào chúng ta có thể chắc chắn rằng khôn tồn tại một tập hợp con người khai thác sẽ quyết định tạo chuỗi khối riêng của họ? Định nghĩa Blockchain là một máy singleton giao dịch với trạng thái chia sẻ.  Sử dụng định nghĩa này, chúng ta có thể hiểu trạng thái hiện tại chính xác là một chân lý toàn cầu duy nhất, mà mọi người đều phải chấp nhận. Có nhiều trạng thái (hoặc chuỗi) sẽ làm hỏng toàn bộ hệ thống, bởi vì sẽ không thể thống nhất được trạng thái nào là đúng. Nếu các chuỗi phân kỳ, bạn có thể sở hữu 10 đồng tiền trên một chuỗi, 20 đồng trên chuỗi khác và 40 đồng trên chuỗi khác. Trong trường hợp này, sẽ không có cách nào để xác định chuỗi nào là "hợp lệ" nhất.

- Bất cứ khi nào nhiều đường dẫn được tạo, một "ngã ba" sẽ xảy ra. Thông thường, chúng tôi muốn tránh fork vì chúng phá vỡ hệ thống và buộc mọi người phải chọn chuỗi mà họ “tin tưởng”.

- Để xác định đường dẫn nào là hợp lệ và ngăn chặn được nhiều chuỗi, Ethereum sử dụng cơ chế được gọi là "GHOST Protocol"
“GHOST” = “Greedy Heaviest Observed Subtree”

Giao thức GHOST cho biết chúng ta phải chọn đường dẫn có nhiều tính toán nhất được thực hiện trên nó. Một cách để xác định đường dẫn đó là sử dụng số khối của khối gần đây nhất("leaf block"), đại diện cho tổng số khối trong đường dẫn hiện tại(không tính khối gốc). Số khối càng cao, đường đi càng dài và nỗ lực khai thác phải bỏ ra đến leaf "lá" càng lớn.

# Các thành phần chính mà hệ thống Ethereum bao gồm:
    - accounts
    - state
    - gas and fees 
    - transactions
    - blocks
    - transaction execution
    - mining
    - proof of wook

    onenote: Ethereum uses the KECCAK-256 hash.

    + accounts : "shared-state"(trạng thái chia sẻ) bao gồm nhiều đối tượng nhỏ("account") có thể tương tác với nhau thông qua một khung truyền thông điệp. Mỗi tài khoản có một trạng thái (stage) được liên kết với nó và có một địa chỉ (address) 20 byte. Địa chỉ trong Ethereum là một số nhận dạng 160 bit được sử dụng để xác định bất kỳ tài khoản nào.
        - Có 2 loại tài khoản: 
            -(Externally owned accounts) Các tài khoản được sở hữu bên ngoài, được kiểm soát bởi các khóa riêng tư và không có mã nào được liên kết với chúng.
            -(Contract accounts) Tài khoản hợp đồng, được kiểm soát bởi mã hợp đồng của họ và có mã được liên kết với chúng.
        Externally owned accounts vs. contract accounts:
            - Tài khoản thuộc sở hữu bên ngoài có thể gửi tin nhắn đến các tài khoản thuộc sở hữu bên ngoài hoặc tới các tài khoản hợp đồng khác bằng cách tạo và ký một giao dịch sử dụng khóa các nhân của tài khoản đó.
            + Không giống như các tài khoản thuộc sở hữu bên ngoài, tài khoản hợp đồng không thể tự bắt đầu các giao dịch mới.

    + account state:
        Trạng thái tài khoản bao gồm 4 thành phần được hiển thị bất kể loại tài khoản nào.
            + nonce : Nếu tài khoản là tài khoản thuộc sở hữu bên ngoài, con số này đại diện cho số lượng giao dịch được gửi từ địa chỉ của tài khoản.