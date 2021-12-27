# Elastic Search là gì ?
* Là một máy chủ web dựa trên JSON , phân tán , được xây dựng trên Lucene. Mặc dù đó là Lucene, người đang thực hiện công việc thực tế bên dưới, Elasticsearch cung cấp cho chúng ta một lớp thuận tiện hơn Lucene. Mỗi phân đoạn được tạo ra trong Elasticsearch là một thể hiện Lucene riêng.
* Nó xây dựng trên Lucence, cung cấp Rest API dựa trên Json.
* Cung cấp hệ thống phân tán trên đỉnh của Lecence.
* Lucence không xây dựng hệ thống phân tán, ES phải làm. ES cung cấp sự trừu tượng hóa của cấu trúc phân tán. 

## Tổng hợp câu lệnh query
### 1. Query DSL (Doamin specific language )
 * Truy vấn đơn (tìm kiếm một giá trị cụ thể trong một field cụ thể ): `match`, `term`, `range`.
 * Truy vấn kép: Bao gồm nhiều câu lệnh truy vấn đơn cùng các truy vấn kép, được sử dụng kết hợp theo một logic hợp lý: Ex: `bool`, `dis_max`.
### 2. Match all query (Lấy all documents)
 * Ex: `{
        "query": {
            "match_all": {}
        }
    }`
 * Kết quả sẽ trả về tất cả document.
### 3. Full text queries
 * Sài trong các field được phân tích từ trước, có các loại phân tích (analyzer) cho mỗi loại field.
 * Match query:
    * Truy vấn chuẩn để thực hiện full text query. Bao gồm truy vấn kết hợp và truy vấn cụm từ gần đúng sài ngày em **match**
    * ex: `{
        "query": {
            "match": {
                "name": "luongndcoder github"
            }
        }
    }`
 - Kết quả: trả ra những record có name là **luongndcoder** và cả **github**
### Match Phrase Prefix Query
* Truy vấn **match_phrase** phân tích văn bản và tạo 1 truy vấn cụm từ:
* Ex: `{
        "query": {
            "match_phrase": {
                "full_name": "Nguyễn Lương"
            }
        }
    }`
* Kết quả của thằng này sẽ trả ra những record có **full_name** là "Nguyễn Lương"
* Thêm một thằng em của nó nữa là: **match_phrase_prefix**, (thêm điều kiện khớp với tiền tố của từ trong văn bản).
    * Ex cái cho nó máu: `{
        "query": {
            "match_phrase_prefix": {
                "full_name": "Lương"
            }
        }
    }`
    * Kết quả trả về là **Lương** và **Lương Nguyễn** cũng có luôn.
### Multi Match Query
* Sài thằng này thì search được nhiều field nhá.
* Ex: `{
        "query": {
            "multi_match": {
                "query": "luong",
                "fields": ["name", "email"]
            }
        }
    }`
* Field có thể chỉ định bằng ký tự đại diện
    * Ex nào: `{
        "query": {
            "multi_match": {
                "query": "luong",
                "fields": ["*_name", "email"]
            }
        }
    }`
    * Thế là đã search được cả các full_name, first_name, cái gì có _name là search được rồi (xịn :D), à cả thằng `email` nữa đấy.
### 4. Term level queries
 * Truy vấn **term** tìm được những record có chứa cụm từ chính xác trong query.
 * Ex: `{
        "query": {
            "term": {
                "full_name": "Nguyễn Danh Lương"
            }
        } 
    }`
    * Ae muốn query list full_name có thể dùng: `{"terms": {"email": ["luongnd@gmail.com", "thiennd@gmail.com"]}}`
 * Kết quả trả về những record có full_name là : **Nguyễn Danh Lương**

### 5. Range Query
 * Trả về các record với trường khớp với phạm vi nhất định.
 * Ex: `{
     "query": {
         "range": {
             "weight": {
                 "lte": 50,
                 "gte": 70
             }
         }
     }
    }`
* Thằng này cho phép truyền các params: 
    * gte: Lớn hơn hoặc bằng
    * gt: Lớn hơn
    * lte: Nhỏ hơn hoặc bằng
    * lt: Nhỏ hơn
* Kết quả là trả ra những record nào nằm trong phạm vi 50 -> 70 kg.
* `Date format in range queries`.
    * Thêm thằng này nữa ae ạ:
        * Ex: `{
            "query": {
                "range": {
                    "created_time": {
                        "gte": "20/08/2000",
                        "lte": "2021",
                        "format": "dd/MM/yyyy||yyyy"
                    }
                }
            }
        }`
* `Wildcard Query`
    * Trả về các record khớp với các ký tự đại diện được đưa ra.
    * Ex: `{
        "query": {
            "wildcard": {
                "full_name": "*Lương*"
            }
        }
    }`
    * Kết quả: Trả về các record có full_name có chữ `Lương`, có thể là `Nguyễn Danh Lương`, `Danh Lương`

### 5. Bool Query
* Cho phép kết hợp các câu lệnh truy vấn khác để tạo một logic hợp lý. Có các loại:
    * **must**: Phải phù hợp với tất cả điều kiện và đóng góp vào điểm số.
    * **filter**: Giống với **must** nhưng bỏ qua điểm số.
    * **should**: Chỉ cần phù hợp với một trong các điều kiện.
    * **must_not**: Ngược lại với **must**, phải không phù hợp với tất cả các điều kiện.
* Ex: `{"query": {
    "bool": {
        "must": {
            "term": {
                "user_name": "luongndcoder"
            }
        },
        "filter": {
            "term": {
                "gender": "male"
            }
        },
        "must_not": {
            "range": {
                "age": {
                    "gte": 21,
                    "lte": 27
                }
            }
        },
        "should": [
            {"term": {"code": "110"}},
            {"term": {"code": "113"}}
        ],
    }
}}`
* kết quả thằng này thì hơi khó giải thích đấy :D, cơ mà nó sẽ như này:
    * Lấy tất cả thằng nào phù hợp với `user_name` bằng "luongndcoder" với `gender` bằng "male" với `age` không nằm trong khoảng 21 đến 27 với `code` phải bằng 110 hoặc 113.
* Bool query in filter context
    * Sài thằng này thì nhớ nếu như có cái mệnh đề `should` thì trong đó phải tồn tại ít nhất một mệnh đề `should` là bắt buộc phù hợp.

## À thằng này là tôi bếch từ [Viblo.asia](https://viblo.asia/p/query-dsl-trong-elasticsearch-Eb85oJq2l2G) về ae có thể bơi vào đây để xem nội dung gốc nhé.
