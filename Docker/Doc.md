## Docker 
- Có 3 Khái niệm quan trọng:
    + Docker file 
    + Docker Image 
    + Docker Container 

    + docker file -> build -> image -> container 
    + Công thức -> Nguyên liệu -> Trà sữa 

- Lệnh docker:
    + Build một image : docker build --tag tag_name
    + Xem list images : docker images 
    + Gắn tag images: docker tag tag_name:latest tag_name:version_name
    + Xóa thẻ images: docker rmi tag_name:version_name
    + Run image docker: docker run image_name
    + Run image public host port: container port : docker run --publish host_port:container_port image_name
    + Run image detached mode (Chế độ tách rời ): docker run -d -p host_port: container_port image_name
    + List container đang chạy : docker ps
    + List all container : docker ps -all (or -a)
    + Stop container: docker stop container_name
    + Restart container : docker restart container_name
    + Remove container: docker rm container_name_1 container_name_2 container_name_3
    + Rest container : docker run -d -p 5000:5000 --name rest-server container_name

    + docker logs [-f^6] container: hiển thị log container output (sdtdout + stderr)
    + docker diff container: hiển thị các differance của image


- Một số lưu ý:
    + Khi cài docker docker sẽ tự khởi tạo một card mạng là bridge -> thực hiện kết nối với card mạng thật(wifi, ethernet) -> đi ra ngoài internet

- 