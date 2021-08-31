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

    - Cryptographic hashing