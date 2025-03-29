# Hướng dẫn sử dụng `wait-for-it.sh` trong Dockerfile ENTRYPOINT

## 1️⃣ Giới thiệu `wait-for-it.sh`
`wait-for-it.sh` là một script Bash giúp kiểm tra xem một service có sẵn sàng trước khi thực thi một lệnh khác. Điều này rất hữu ích trong Docker khi một container cần chờ một service khác (ví dụ: database) trước khi khởi chạy.

---

## 2️⃣ Cách tải `wait-for-it.sh`
Bạn có thể tải script này về bằng lệnh sau:
```sh
curl -o wait-for-it.sh https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh
chmod +x wait-for-it.sh
```
Hoặc thêm trực tiếp vào `Dockerfile`:
```dockerfile
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /usr/local/bin/wait-for-it
RUN chmod +x /usr/local/bin/wait-for-it
```

---

## 3️⃣ Cách sử dụng `wait-for-it.sh` trong Docker ENTRYPOINT

### 📌 Ví dụ 1: Chờ MySQL sẵn sàng trước khi khởi chạy ứng dụng
```dockerfile
FROM python:3.9

WORKDIR /app

COPY . /app
COPY wait-for-it.sh /usr/local/bin/wait-for-it
RUN chmod +x /usr/local/bin/wait-for-it

ENTRYPOINT ["wait-for-it", "db:3306", "--timeout=30", "--", "python", "app.py"]
```
👉 Lệnh trên đảm bảo **`app.py` chỉ chạy sau khi MySQL (db:3306) sẵn sàng**.

---

### 📌 Ví dụ 2: Sử dụng `wait-for-it.sh` trong `docker-compose.yml`
Nếu bạn có một **service cần chờ database**, bạn có thể chỉnh sửa `entrypoint` như sau:

#### 📝 `docker-compose.yml`
```yaml
version: '3'
services:
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: example
  app:
    build: .
    depends_on:
      - db
    entrypoint: ["wait-for-it", "db:3306", "--timeout=30", "--", "python", "app.py"]
```
💡 **`depends_on` không kiểm tra nếu DB đã khởi động hoàn toàn**, vì vậy `wait-for-it.sh` giúp đảm bảo **ứng dụng chỉ khởi động khi database đã sẵn sàng**.

---
