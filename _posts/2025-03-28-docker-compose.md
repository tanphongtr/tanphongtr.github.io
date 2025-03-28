---
layout: post
title: Docker Compose
---

Docker Compose là một công cụ mạnh mẽ giúp bạn dễ dàng định nghĩa và chạy các ứng dụng Docker có nhiều container. Thay vì phải chạy từng container riêng lẻ và liên kết chúng bằng tay, bạn có thể sử dụng Docker Compose để quản lý tất cả trong một tệp YAML duy nhất.

## Cấu trúc tệp `docker-compose.yml`

Tệp `docker-compose.yml` giúp bạn định nghĩa cấu hình của các container. Dưới đây là một ví dụ đơn giản:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  database:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: example
```

## Cách sử dụng Docker Compose

### 1. Cài đặt Docker Compose

Bạn có thể cài đặt Docker Compose bằng lệnh sau (với Linux/macOS):
```sh
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### 2. Khởi động các dịch vụ

Chạy lệnh sau trong thư mục chứa `docker-compose.yml`:
```sh
docker-compose up -d
```
Lệnh này sẽ chạy các container ở chế độ nền.

### 3. Dừng và xóa các container

```sh
docker-compose down
```
Lệnh này sẽ dừng và xóa tất cả các container được quản lý bởi Docker Compose.

## Lợi ích của Docker Compose

✅ Dễ dàng quản lý nhiều container cùng lúc.  
✅ Tự động hóa việc cấu hình mạng giữa các container.  
✅ Dễ dàng mở rộng hệ thống bằng cách chỉnh sửa `docker-compose.yml`.  

![Docker Compose]({{ site.baseurl }}/images/docker-compose.png)

Bạn có thể tìm hiểu thêm về Docker Compose trong [tài liệu chính thức của Docker](https://docs.docker.com/compose/).

