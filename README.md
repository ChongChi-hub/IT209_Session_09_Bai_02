# Báo cáo Bài 2: Khởi chạy Web Server Nginx với Port Mapping

## 1. Mục tiêu
- Khởi chạy một Web Server Nginx dạng container chạy ngầm (detached mode `-d`).
- Thực hiện cơ chế ánh xạ cổng mạng (Port Mapping `-p`) từ máy chủ host vào bên trong container.
- Kiểm tra kết nối dịch vụ web thông qua lệnh `curl` và tiến hành dọn dẹp (stop & remove container) sau khi hoàn tất.

## 2. Các bước thực hiện và lệnh đã sử dụng

### Bước 1: Khởi chạy Nginx container
Sử dụng image `nginx:alpine`, đặt tên container là `my-web`, ánh xạ port `8080` trên máy host vào port `80` của container:
```bash
docker run -d -p 8080:80 --name my-web nginx:alpine
```

### Bước 2: Kiểm tra trạng thái container đang chạy
```bash
docker ps
```

### Bước 3: Gửi truy vấn HTTP kiểm tra trang web
```bash
curl http://localhost:8080
```

### Bước 4: Dừng và xóa container dọn dẹp môi trường
```bash
docker stop my-web && docker rm my-web
```

---

## 3. Nhật ký kết quả đầu ra thực tế từ Terminal

### 3.1. Kết quả khởi chạy container
```text
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
e72112c14215: Pulling fs layer
745dfb2690dd: Pulling fs layer
d9aae54b5831: Pulling fs layer
6c53d0b2a666: Pulling fs layer
64c8194480fe: Pulling fs layer
9a9a644fdd6a: Pulling fs layer
e76228b47809: Pulling fs layer
0deea27e58d9: Download complete
d54d3939625e: Download complete
d9aae54b5831: Download complete
6c53d0b2a666: Download complete
e76228b47809: Download complete
64c8194480fe: Download complete
9a9a644fdd6a: Download complete
d9aae54b5831: Pull complete
6c53d0b2a666: Pull complete
745dfb2690dd: Download complete
745dfb2690dd: Pull complete
e76228b47809: Pull complete
64c8194480fe: Pull complete
9a9a644fdd6a: Pull complete
e72112c14215: Download complete
e72112c14215: Pull complete
Digest: sha256:df221db836e1754089190208cee7eeda94f233197056426eda74a43ab1abeac2
Status: Downloaded newer image for nginx:alpine
391edd2524f30dbfe2ab215688994558f8f5ab422dbc960b3f534fcd73e8f3cf
```

### 3.2. Kết quả kiểm tra bằng `curl http://localhost:8080`
```text
HTTP/1.1 200 OK
Server: nginx/1.31.6
Date: Mon, 12 Oct 2026 12:57:57 GMT
Content-Type: text/html
Content-Length: 896
Last-Modified: Tue, 15 Sep 2026 14:18:52 GMT
Connection: keep-alive
ETag: "6aa953cc-380"
Accept-Ranges: bytes

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy, 
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional 
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

### 3.3. Kết quả dọn dẹp container
```text
my-web
my-web
```

---

## 4. Giải thích ý nghĩa các tham số lệnh Docker

| Tham số | Ý nghĩa |
| :--- | :--- |
| `-d` (`--detach`) | Chạy container ở chế độ nền (ngầm), giải phóng terminal ngay sau khi khởi chạy. |
| `-p 8080:80` (`--publish`) | Ánh xạ cổng (Port Forwarding): Cổng `8080` trên máy chủ host kết nối vào cổng `80` (cổng HTTP mặc định của Nginx) bên trong container. |
| `--name my-web` | Đặt tên định danh tường minh cho container là `my-web` giúp dễ dàng quản lý thay vì dùng ID ngẫu nhiên. |
| `nginx:alpine` | Image gốc được sử dụng, dựa trên hệ điều hành Alpine Linux siêu nhẹ giúp tiết kiệm dung lượng đĩa và tài nguyên RAM/CPU. |

---

## 5. Hướng dẫn chụp ảnh minh chứng & Placeholder
1. Mở Terminal và chạy tuần tự các lệnh khởi chạy và kiểm tra:
   ```bash
   docker run -d -p 8080:80 --name my-web nginx:alpine
   docker ps
   curl http://localhost:8080
   ```
2. Chụp ảnh màn hình hiển thị container `my-web` trong danh sách `docker ps` và kết quả trả về `Welcome to nginx!` của lệnh `curl`.
3. Dán ảnh vào vị trí placeholder bên dưới:

`ImgEx`
