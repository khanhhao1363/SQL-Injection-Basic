# SQL Injection Basic

> Tên Tài Liệu: SQL Injection Basic

> Người Thực Hiện: Nguyễn Khánh Hào

> Cập Nhật Lần Cuối: 10/9/2024

# Mục Lục


# 1. Định Nghĩa và Cách Phát Hiện

Định Nghĩa: SQL Injection là loại lỗ hổng cho phép attacker có thể chèn các câu lệnh SQL độc hại và thao túng cơ sở dữ liệu, từ đó có thể trích xuất được credentials của mục tiêu hoặc cũng có thể sửa đổi hoặc xóa các dữ liệu nhạy cảm trong hệ thống.

SQL Injection bao gồm:

`In-band SQLi`:

Error-based SQLi: phụ thuộc vào kết quả lỗi trả về.

Union-based SQLi: gợp các câu truy vấn lại với nhau để có thể truy xuất database.

`Blind SQLi`:

Boolean-based SQLi: dạng tấn công này dựa theo kết quả trả về của phản hồi.

Time-based SQLi: dựa theo thời gian trả về của phản hồi.

`Out-of-band SQLi`:

có thể nhận dữ liệu từ cơ sở dữ liệu thông qua các yêu cầu HTTP, DNS.

Cách Phát hiện:

Có thể sử dụng các ký tự như `'`, `"`, `--`, `;` để kiểm tra có lỗi syntax trả về hay không.
Với boolean thì có thể sử dụng `OR 1=1` và `OR 1=2` để xem kết quả trả về là true hay false.
Có thể sử dụng các tools như : Burp scan, sqlmap, sqlmc.

# 2. Lỗi SQL Injection trên các hàm SELECT, INSERT, UPDATE, DELETE

`SELECT Injection`:

```SQL
SELECT * FROM users WHERE username = 'admin' OR '1'='1';
```
Câu lệnh sẽ trả về tất cả các dữ liệu trong bảng users nếu điều kiện luôn đúng.

`INSERT Injection`:

```SQL
INSERT INTO users (username, password) VALUES ('admin', 'password'); DROP TABLE users; --';
```

`UPDATE Injection`:

```SQL
UPDATE users SET password = 'newpassword' WHERE username = 'admin' OR '1'='1';
```

`DELETE Injection`:

```SQL
DELETE FROM users WHERE username = 'admin' OR '1'='1';
```

# Khuyến Nghị Khắc Phục

1. Sử dụng Prepared Statements để an toàn trước các cuộc tấn công SQL Injection.

2. Implement việc lọc và validate input của người dùng.

3. Hạn chế quyền hạn của database.

4. Triển khai Web Application Firewall (WAF) để phát hiện và chặn các tấn công SQL Injection.
