## Web Service Gin Gonic
- Là một cái FrameWork code API bằng Golang với hiệu xuất nhanh. Rõ ràng và tinh gọn.

## Vào món chính (Tutorial thôi nhé :D)
- Viết vài cái API CRUD nhẹ nhẹ để hiểu nó thôi nhể, quẩy thôi nào :D
- Tạo ra một thư mục (Project) chứa code đã rồi **cd** vào thư mục đó nhé.
    ```bash
    $ cd /Documents/golang
    $ mkdir golang-gin-gonic
    $ cd golang-gin-gonic
    $ go mod init
    $ go get -u github.com/gin-gonic/gin
    $ code . (để mở VS Code nhé :D, nếu ko mở được thì mở tay nhé :D)
    ```
- Giờ thì tạo một file **main.go** để code thôi nào.
    - Giờ thì khởi tạo một cái API để ping đã nhỉ :D
        ```golang
        package main

        import (
            "net/http"

            "github.com/gin-gonic/gin"
        )

        func ping(ctx *gin.Context) {
            ctx.JSON(http.StatusOK, gin.H{
                "messge": "Pong",
            })
        }

        func main() {
            router := gin.Default()
            router.GET("/ping", ping)
            router.Run("localhost:8080")
        }
        ```
    - Trên terminal run go file **main.py** để start server nàooooo
        ```bash
        $ go run main.go

        [GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

        [GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
        - using env:   export GIN_MODE=release
        - using code:  gin.SetMode(gin.ReleaseMode)

        [GIN-debug] GET    /ping                     --> main.ping (3 handlers)
        [GIN-debug] [WARNING] You trusted all proxies, this is NOT safe. We recommend you to set a value.
        Please check https://pkg.go.dev/github.com/gin-gonic/gin#readme-don-t-trust-all-proxies for details.
        [GIN-debug] Listening and serving HTTP on localhost:8080
        ```
        - Hiển thị như trên có nghĩa là thành công rồi nhé!
        - Call thử xem nào (Trả data như dưới là được rồi nhé :D) 
        ```bash
        $ curl http://0.0.0.0:8080/ping
        
        {"messge":"Pong"}%
        ```
