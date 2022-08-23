#  Thay đổi cổng kết nối SSH từ 22 thành 2022
Đầu tiên, chúng ta cần xác định dịch vụ SSH đã được cài đặt trên máy chủ:

**$ sudo systemctl status ssh**

Tiếp đến chúng ta phải kiểm tra để chắc chắn rằng SSH đang được chạy trên cổng mặc định:

**$ sudo netstat -pnltu | grep 22**

_Tuy nhiên, khi chạy lệnh này nếu hệ thống báo lỗi sudo: netstat: command not found, thì có nghĩa chúng ta chưa cài đặt lệnh Netstat trên Linux, chúng ta có thể sử dụng lệnh sau để cài đặt_

_**$ sudo apt install net-tools**_

Khi đã chắc chắn đã chạy trên cổng mặc định, chúng ta sẽ bắt đầu điều chỉnh cổng truy cập. Các cổng TCP nằm trong khoảng từ cổng 0 - 65535:

**$ sudo vim /etc/ssh/sshd_config**

Tìm dòng bắt đầu bằng #Port 22, sau đó bỏ dấu # và điều chỉnh thành Port 2022

Sau khi đã thay đổi, chúng ta cần restart lại dịch vụ SSH

**$ sudo systemctl restart ssh**

Chúng ta có thể kiểm tra lại một lần nữa xem dịch vụ SSH đã được chạy trên cổng 2022 chưa

**$ sudo netstat -pnltu | grep 2022**

# Giới hạn kết nối IP truy cập SSH #

**$ vi /etc/hosts.allow**

Thêm IP tòa nhà: *sshd: 118.69.62.113*

**$ vi /etc/hosts.deny**

Chặn toàn bộ các IP khác ngoài IP tòa nhà: *sshd: ALL*

s# Cấu hình Firewall với UFW với các cổng cho phép

Bật Firewall

**$ sudo ufw enable**

Cho phép cổng kết nối

**$ sudo ufw allow port**

Các port phổ biến 

20	ftp-data	File Transfer [Default Data]

21	ftp	File Transfer [Control]

22	Ssh	SSH Remote Login Protocol

23	telnet	Telnet

25	Smtp	Simple Mail Transfer

53	Domain	Domain Name Server

80	www-http	World Wide Web HTTP

110	POP3 (non-secure)	Post Office Protocol – Version 3

995	POP3 (secure)	Post Office Protocol Secure

143	IMAP (non-secure)	Internet Message Access Protocol

993	IMAP (secure)	Internet Message Access Protocol

465	Smtp (SSL)	Simple Mail Transfer with SSL

587	Smtp (TLS)	Simple Mail Transfer with TLS

443	https	HTTP Secure

# Chỉnh sửa Hostname theo chuẩn FQDN #

Kiểm tra Hostname đang sử dụng

**$ sudo hostname**

Đổi Hostname

**$ sudo hostname teammailonly.xyz**

Đổi File Hostname

**$ sudo vi /etc/hostname**

Đổi File Host

**$ sudo vi /etc/hosts**

Reboot server

**reboot**

# Thay đổi Timezone #

Kiểm tra múi giờ hiện tại

**date**

Thay đổi múi giờ Hồ Chí Minh

**timedatectl set-timezone Asia/Ho_Chi_Minh**

Xem danh sách múi giờ thế giới 

**timedatectl list-timezones | grep Asia**

# Cài đặt mô hình LAMP #

Đầu tiên cần phải tiến hành cập nhật các gói (package) đã được cài đặt trên hệ thống Ubuntu

**sudo apt update -y && apt upgrade -y**

## Cài đặt Web Server Apache ##

Máy chủ web Apache là một trong những máy chủ web phổ biến nhất trên thế giới. Nó đã được ghi chép đầy đủ và được sử dụng rộng rãi trong một thời gian dài, điều này khiến cho Apache trở thành một lựa chọn mặc định tuyệt vời để lưu trữ một website.

Cài đặt apache2 và apache2-utils để tích hợp một số tiện ích cho Apache HTTP

**sudo apt install -y apache2**

Kiểm tra phiên bản (version) của Apache.

**apache2 -v**

Kiểm tra hoạt động Apache

**Bây giờ  hãy ra trình duyệt và truy cập bằng IP máy chủ của mình để kiểm tra. Nếu hiển thị trang Apache2 Default Page như bên dưới là thành công.**

*Lưu ý: Mở Port 80 (HTTP) với tường lửa*

## Cài đặt MariaDA Database Server ##

MariaDB là bản thay thế cho MySQL. Nó được phát triển bởi các thành viên cũ của nhóm MySQL. 

**sudo apt install -y mariadb-server mariadb-client**

Thiết lập nâng cao cho Mariadb

Bây các  sẽ cài đặt mật khẩu root cho Mariadb và thiết lập một số tùy chỉnh khác với lệnh

**sudo mysql_secure_installation**

Kiểm tra phiên bản (version) của Mariadb.

**mariadb --version**

## Cài dặt PHP ##

Thêm gói PPA (ondrej/php) để cài đặt PHP 8.1 và các modules cần thiết cho Apache

**sudo apt install software-properties-common**

**sudo add-apt-repository ppa:ondrej/php**

**sudo apt install -y php8.1 libapache2-mod-php8.1**

**sudo apt install php-net-ldap2 php-net-ldap3 php-imagick php8.1-common php8.1-gd php8.1-imap php8.1-mysql php8.1-curl php8.1-zip php8.1-xml php8.1-mbstring php8.1-bz2 php8.1-intl php8.1-gmp php8.1-redis**

Kiểm tra phiên bản (version) của PHP.

**php -v**

Để kiểm tra các PHP với máy chủ Apache, chúng ta cần tạo một  info.php tại Document root của Apache với lệnh bên dưới

**sudo vi /var/www/html/info.php**

Sau đó nhập nội dung dưới đây và save lại:

*<?php

phpinfo();

?>*

Tiếp đó  vào trình duyệt và truy cập theo đường dẫn: http://IPServer/info.php để kiểm tra. Nếu hiển thị PHP là thành công.

## Cài đặt phpMyAdmin ##

phpMyAdmin là ứng dụng dùng để quản lý cơ sở dữ liệu dưới dạng giao diện, thông qua phpMyAdmin sẽ giúp bạn quản lý các Database trực quan hơn. Để cài đặt  hãy thực hiện như sau:

**sudo apt install -y phpmyadmin**

*Tiếp đến chọn apache2 và nhấn Enter*

*Tại giao diện tiếp theo,  chọn Yes để cấu hình cơ sở dữ liệu cho phpMyAdmin với dbconfig-common.*

*Bây giờ tạo mật khẩu mới cho user phpmyadmin và nhấn nút Tab để chuyển sang OK và nhấn Enter.*

*Tiếp tục nhập lại mật khẩu và nhấn nút Tab để chuyển sang OK và nhấn Enter.*


Thêm các đặc quyền cho user phpmyadmin

**sudo mysql -u root 
show grants for phpmyadmin@localhost;
exit;**

Cấu hình để truy câp phpMyAdmin

Sau khi cài đặt phpMyAdmin, cần cấu hình nó với Apache để có thể truy cập vào giao diện web.

**sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf**

**sudo a2enconf phpmyadmin.conf**

**sudo systemctl reload apache2**


Kiểm tra hoạt động phpMyAdmin

Sau khi cấu hình xong, vào trình duyệt và truy cập theo đường dẫn http://IP_Server/phpmyadmin để truy cập phpMyAdmin. Nếu thành công, giao diện sẽ hiển thị khung đăng nhập, và  sẽ sử dụng thông tin đã tạo ở phần Cài đặt phpMyAdmin đăng nhập vào.








    















