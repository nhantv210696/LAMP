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

**$ sudo systemctl restart ssh***

Chúng ta có thể kiểm tra lại một lần nữa xem dịch vụ SSH đã được chạy trên cổng 2022 chưa

**$ sudo netstat -pnltu | grep 2022**

# Chuyển đổi xác thực SSH bằng Key thay cho mật khẩu (Tắt xác thực SSH bằng mật khẩu) #

## Tắt xác thực SSH bằng mật khẩu ##
Thao tác này sẽ được thực hiện trong file /etc/ssh/sshd_config.

Đầu tiên sẽ vào thư mục /etc/ssh/sshd_config bằng trình soạn thảo văn bản 

**$ sudo nano /etc/ssh/sshd_config**

Kéo xuống và tìm dòng "PasswordAuthentication yes" 

Có thể sử dụng tổ hợp phím CTRL + X sau đó gõ tìm PasswordAuthentication yes

**Xóa dấu # và chỉnh yes thành no**

Sau khi đã điều chỉnh thì sử dụng tổ hợp phím CTRL + X để thoát

Restart lại SSH

**$ sudo syntemctl restart ssh**

Lúc này xác thực bằng mật khẩu khi đăng nhập vào SSH đã được tắt

## Chuyển đổi xác thực SSH bằng Key ##








