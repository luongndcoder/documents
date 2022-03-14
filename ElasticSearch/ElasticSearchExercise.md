# ElasticSearch Exercise
* **API** : host:port (base khi install trên máy local là http://localhost:9200)
## Add Index
* Add Index API: **API/{index_name}/{type_name}**
    * index_name = "Tên index"
    * type_name = "Loại chỉ mục"
        * Loại chỉ mục thích đặt tên là gì đều được, loại chỉ mục giúp phân biệt loại dữ liệu nằm trong chỉ mục đó. VD: Bạn muốn dùng một chỉ mục cho toàn bộ dữ liệu bán hàng của bạn. 
        * Có dữ liệu người dùng, đơn hàng, thông tin sản phẩm có thể tạo ra từng loại chỉ mục để mapping với các dữ liệu đó.
        * VD: index_name = "ecommere", gồm có các index_type là (product: TT sản phẩm, salesorder: Thông tin đơn hàng, user: TT khách hàng, vv)
## Get mapping field index
* Get mapping field API: **API/{index_name}/_mapping**
    * Lấy ra thông tin mapping các field của index trên elasticsearch
    * Thông tin bao gồm loại index(type), danh sác field trong và kiểu dữ liệu trong từng field

## Query DSL(Domain Specific Language)
* Query DSL API: **API/{index_name}/_search**
    * Query DSL dựa trên JSON để định nghĩa các truy vấn. Có thể coi Query DSL là một Abstract Syntax Tree của các truy vấn
    * Match all Query
        ```
        {
            "query": {
                "match_all": {}
            }
        }
        ```
    * Match None query (Nghịch đảo với **match_all**)
        ```
        {
            "query": {
                "match_none": {}
            }
        }
        ```
    * Match Query
        ```
        "query": {
            "match": {
                "first_name": {
                    "query": value
                }
            }
        }
        ``
    * Match Phrase Prefix
        ```
        {
            "query": {
                "first_name": {
                    "query": value
                }
            }
        }
        ```
    * Multi Match Query
        ```
        {
            "query": {
                "multi_match": {
                    "query": value,
                    "fields": ["filed_name_1", "field_name_2", "field_name_...."]
                }
            }
        }
        ```
    * Term query
        * Trả về các document mà field được chỉ định có giá trị đúng bằng term truyền vào
        ```
           {
               "query": {
                   "term": {
                       "id": 228
                   }
               }
           } 
        ```
    * Tránh sử dụng term query trên ```text``` field vì mặc định Elasticsearch sẽ thay đổi giá trị của text field tròng quá trình phân tích làm cho việc tìm kiếm giá trị chính xác của text field sẽ khó.
        * VD: 
            ```
            {
                "query": {
                    "term": {
                        "first_name": "Benedikta"
                    }
                }
            }
            ```
        * Thực hiện lấy tất cả bản ghi với first_name sẽ không trả về bản ghi nào
        ![alt text](https://i.imgur.com/C4lmWxt.png "Title")
        * Thực hiện query bằng **match** đã ra kết quả
        ![alt text](https://imgur.com/84VYXev.png "Title")

    * Range Query
        * Trả về các document chứa các term nằm trong phạm vi chỉ định
            ```
            {
                "query": {
                    "range": {
                        "id": {
                            "gte": 10,
                            "lte": 12
                        }
                    }
                }
            }
            ```
            * Kết quả trả về:
            ![alt text](https://imgur.com/a6evVdo.png)
    