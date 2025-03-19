<h1>What is Docker</h1>

Docker is an opening platform for developing, shipping and running applications. Docker enables you to separate
your applications form infrastructure so you can deliver software quickly.  
Docker provides the ability to package and run an application in a loosely isolated environment called a container. 

<h1>Docker Architecture</h1>  


![image](https://github.com/user-attachments/assets/39af12c1-1198-4c42-bdb5-95e2717a11c5) 


Docker use client-server arrchitecture. The docker client talks to Docker daemon. which does heavy lifting or
building,running, distributing your Docker containers. Client and daemon(host) can run on same system, or you can
connect a Docker client to a remote Docker daemon.  
Communicate between daemon and client using REST API, over UNIX socket or a network interface. 
Another Docker client is Docker Compose, that lets your work with applications consisting of a set of containers.

<h1>Docker Registry</h1>
Docker hub. When do `docker pull` or `docker run` Docker pulls all the required images from configured registry.  
`docker push` to push image to registry.

<h2>Command</h2>

`docker run` to start a container  

`docker build` building a image  

`docker image ls` show all image   

`docker ps` show all container  

  
EX:  
`docker run -d --name my_container -p 8080:80 nginx`  
`-d` → Chạy ở chế độ nền (detached)  
`--name my_container` → Đặt tên cho container  
`-p 8080:80 `→ Mở cổng 8080 trên host và ánh xạ vào cổng 80 trong container  
`nginx` → Image để chạy container  

`docker stop my_container `       # Dừng container  
`docker start my_container `      # Khởi động lại container  
`docker restart my_container  `   # Restart container  
`docker rm my_container `         # Xóa container (phải dừng trước)  
`docker rm -f my_container `      # Xóa container kể cả khi đang chạy  
`docker rm $(docker ps -aq) `     # Xóa toàn bộ container  

`docker exec -it my_container bash`   # Mở shell trong container  
`docker logs my_container `           # Xem log của container  
`docker top my_container `            # Xem tiến trình trong container  
`docker stats my_container   `        # Theo dõi tài nguyên container (CPU, RAM)   

Các container trong cùng network mới có thể giao tiếp với nhau.

`docker network create my_network` # tạo network  
`docker network connect my_network my_container` # connect container vào network   
`docker network rm my_network  ` 

`docker volume create my_volume ` # tạo volumn  
`docker volume rm my_volume`   

`docker volume prune `  # Xóa tất cả volume không sử dụng  

Các lệnh cleanup: (chưa dùng bao h)
`docker system prune `        # Xóa container, image, network không sử dụng  
`docker system prune -a `     # Xóa tất cả container, image (kể cả dùng trước đây)  
`docker volume prune  `       # Xóa tất cả volume không sử dụng  

**Tổng kết**  
✔ Container: run, ps, stop, rm, logs, exec  
✔ Image: pull, build, commit, rmi  
✔ Network: network create, network connect, network ls  
✔ Volume: volume create, volume rm, volume prune  
✔ Cleanup: system prune, volume prune  

<h1>Docker Compose</h1>  
Nếu muốn chạy nhiều container, phải có cách kết nối chúng lại với nhau. Giờ nếu như cũ ta phải build từng container
cho database, message queue, cache,... Chưa hết ta còn cần quản lý mạng để các container kết nối dược với nhau. Sau khi hoàn tất những điều này
ta còn phải clean nó đi.   

Với Docker Compose, chúng ta định nghĩa tất tần tật container và cấu hình của chúng trong 1 file `YAML ` # Yet Another Markup Language (Vua đặt tên)   

Compose là 1 công cụ khai báo. Sau khi khai báo xong chỉ cần chạy `docker compose up`   

Nếu có thay đổi, chạy lại ` docker compose up` và thay đổi sẽ tự được điều chỉnh   

  
Dockerfile vs Compose file.  

Dockerfile là hướng dẫn để docker daemon build image, còn Compose xác định các container để chạy. Thường thì tệp Compose 
tham chiếu tới Dockerfile để build image cho 1 service cụ thể.  

`docker compose down` sẽ xoá mọi thứ tạo lên bằng up. Mặc định thì volumns không tự động bị xoá khi ta down Compose.
Nếu muốn xoá thì phải thêm cờ --volumns vào lệnh. `docker compose down --volumns`  
(thích thì xoá bằng GUI cho dễ k cần nhớ gì)  
<h2>Compose file</h2>  
mặc định cho tệp compose là `compose.yaml` hoặc `.yml` cũng có thể là `docker-compose.yaml` hay`.yml`
nhưng nếu cả 2 đều có trong project thì Compose ưu tiên tệp `compose.yaml`  

ví dụ:  
![image](https://github.com/user-attachments/assets/7bf484cf-09ee-4de9-9051-87f285ffd86d)  
Ứng dụng mẫu bao gồm các phần sau:  
<ul>
  <li>2 dịch vụ được hỗ trợ bởi hình ảnh Docker: webapp và database  </li>
  <li>1 secrets (HTTPS certificate), được đưa vào giao diện người dùng  </li>
  <li>1 cấu hình (HTTP), được đưa vào giao diện người dùng  </li>
  <li>1 ổ đĩa cố định, được gắn vào phần cuối  </li>
  <li>2 mạng</li>
</ul>

đây là file `.yaml` cấu hình cho kiến trúc ứng dụng trên:  

```
services:
  frontend:
    image: example/webapp
    ports:
      - "443:8043"
    networks:
      - front-tier
      - back-tier
    configs:
      - httpd-config
    secrets:
      - server-certificate

  backend:
    image: example/database
    volumes:
      - db-data:/etc/data
    networks:
      - back-tier

volumes:
  db-data:
    driver: flocker
    driver_opts:
      size: "10GiB"

configs:
  httpd-config:
    external: true

secrets:
  server-certificate:
    external: true

networks:
  # The presence of these objects is sufficient to define them
  front-tier: {}
  back-tier: {}
```

  Trong file này có nhiều cấu hình mình chưa dùng bao giờ nên có hơi mơ hồ về secret và config.  
  
  Nói chung để cấu hình để có thể deploy ra bên ngoàn nên để `external: true`  

  `image: example/webapp` nó sẽ tìm xem trong máy có image này không nếu không nó kéo về từ dockerhub(nếu có)  
  có thể build thằng bằng `build: context: //path-to...(Dockerfile)`  

  


