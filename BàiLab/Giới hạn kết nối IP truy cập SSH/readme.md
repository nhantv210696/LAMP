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