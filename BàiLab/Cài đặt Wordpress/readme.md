# Cài đăt Wordpress cơ bản bằng mô hình LAMP #

Vào thư mục HTML

**sudo cd /var/www/html**

Tải và giải nén file cài đặt Wordpress

**sudo wget https://wordpress.org/latest.zip** (tải file)

**sudo unzip lates.zip** (giải nén file)

Nếu thực hiện lệnh giải nén và báo lỗi chưa có lệnh unzip thì có nghĩa chưa cài đặt unzip, có thể dùng lệnh sau để cài đặt

**sudo apt-get install unzip**

Vào thư mục Wordpress

**sudo cd wordpress**

Di chuyển toàn bộ dữ liệu ra ngoài thư mục 

**mv [*]..**

Tạo database trong MySQL


create database vannhan;

CREATE USER 'vannhan'@'localhost' IDENTIFIED BY '123456';

GRANT ALL ON wordpress.* TO 'vannhan'@'localhost' WITH GRANT OPTION;

FLUSH PRIVILEGES;
EXIT;
