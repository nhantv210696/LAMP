# Chuyển SSH Key và tắt đăng nhập bằng mật khẩu #

Tạo file SSH Key (bao gồm public key và private key)

**sudo ssh-keygen**

Generating public/private rsa key pair.
Enter file in which to save the key (/home/nhantv/.ssh/id_rsa):
/home/nhantv/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/nhantv/.ssh/id_rsa
Your public key has been saved in /home/nhantv/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:DtUkER6s2nXjDMyeQSvLSpzrRmspUz0E0jd6J+lQFn0 nhantv@teammailonly.xyz
The key's randomart image is:
+---[RSA 3072]----+
|   .  .+=o.      |
|  . o =.+=E      |
|   . * Boo.      |
|    o B.O o      |
|   . @.BSB .     |
|    B Boo o      |
|   + = ..        |
|  o B            |
|   *.            |
+----[SHA256]-----+

 Key vừa khởi tạo sẽ nằm trong thư mục
        
        Your identification has been saved in /home/nhantv/.ssh/id_rsa
        Your public key has been saved in /home/nhantv/.ssh/id_rsa.pub

Copy SSH key vừa khởi tạo vào server
        ssh-copy-id -p 2022 nhantv@teammailonly

Tắt xác thực bằng mật khẩu 

**sudo vi/etc/ssh/sshd_config**

Sửa lại dòng

_PasswordAuthentication no_
_PermitRootLogin no_

Restart lại SSH

**sudo systemctl restart sshd**

Nếu truy cập SSH với mremote thêm 2 dòng sau vào file sshd_config

_HostKeyAlgorithms +ssh-rsa_
_PubkeyAcceptedKeyTypes +ssh-rsa_

Copy file private key ra máy tính

**sudo cat /home/nhantv/.ssh/id_rsa**

copy toàn bộ file private key ra ngoài notepad++ và save lại theo định dang .ppk

Tải PuttyGen về để import file Private Key

Putty >> SSH >> Auth >> Browse đến file lưu Private Key .ppk trước đó đã lưu

Vào Session nhập IP server, Port, tên session và Save lại.

Load file Session vừa save để kiểm tra xem file Public Key và Private Key đã khớp với nhau chưa, nếu khớp thì sẽ đăng nhập được bằng SSH Key





