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