# Session 07 - Exercise 3: Systemd Service cho Spring Boot

## 1. Cấu hình

* Database: `springboot_db`
* MySQL User: `spring-admin`
* Linux User chạy ứng dụng: `spring-runner`
* File JAR: `/opt/spring-app/app.jar`
* Port: `8082`

## 2. Kiểm tra Systemd Service

Lệnh:

```bash
sudo systemctl status spring-app.service --no-pager
```

Kết quả:

```text
Active: active (running)
Main PID: 4224 (java)
```

Java application được chạy bởi systemd với user `spring-runner`.

## 3. Kiểm tra Port 8082

Lệnh:

```bash
sudo ss -tlnp | grep 8082
```

Kết quả:

```text
LISTEN 0 100 *:8082 *:* users:(("java",pid=4224,fd=9))
```

Port `8082` đang được Java quản lý.

## 4. Kiểm tra User chạy tiến trình

Lệnh:

```bash
ps -o user,pid,cmd -p 4224
```

Kết quả:

```text
USER         PID CMD
spring-runner 4224 /usr/bin/java -jar /opt/spring-app/app.jar
```

## 5. Kết luận

Spring Boot application đã được cấu hình chạy bằng Systemd, sử dụng user `spring-runner` và lắng nghe trên port `8082`.
