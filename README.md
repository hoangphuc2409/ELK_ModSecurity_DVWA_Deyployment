# ELK stack + ModSecurity + DVWA Lab
## Tổng quan
## Topology
## Triển khai
### 1. Cài đặt DVWA
#### 1.1 Tạo DVWA Apache website
Truy cập vào thư mục `/var/www/html` chứa mã nguồn Apache Server và clone repo DVWA vào đây.
```
cd /var/www/html
git clone https://github.com/digininja/DVWA.git
```
Thay đổi permission và khởi động `apache2` service
```
sudo chmod 777 DVWA
sudo service apache2 start
```
Truy cập `http://127.0.0.1/` trên browser để kiểm tra kết quả, nếu xuất hiện hình ảnh này thì đã cài đặt thành công.

![Alt text](Image/setup_apache2.jfif)

Copy nội dung file `config.inc.php.dist` vào file `config.inc.php`
```
cd DVWA
sudo cp config/config.inc.php.dist config/config.inc.php
```
#### 1.2 Tạo DVWA user
Truy cập vào file `config.inc.php` để thay đổi username và mật khẩu. Ở đây, ta đặt username = 'admin' và password = 'password'
```
sudo nano config/config.inc.php
```
![Alt text](Image/dvwa_user.jfif)

Khởi động `mysql` service
```
sudo service mysql start
```
Truy cập với quyền root
```
sudo mysql -u root -p
```
Thực hiện các câu lệnh sau để tạo user
```
create database dvwa;
create user 'admin'@'127.0.0.1' identified by 'password';
grant all on dvwa.* to 'admin'@'127.0.0.1';
exit
```
Vào thư mục `/etc/php/8.2/apache2` và cấu hình file `php.ini`, thay đổi `allow_url_fopen = On` và `allow_url_include = On`
```
cd /etc/php/8.2/apache2
sudo nano php.ini
```
Khởi động lại `apache2` service
```
systemctl restart apache2
```
Truy cập vào `http://127.0.0.1/DVWA` và đăng nhập bằng tài khoản đã tạo -> click `Create/Reset Database`. Cài đặt thành công sẽ có kết quả như hình bên dưới.

![Alt text](Image/DVWA_successfully.jfif)
### 2. Cấu hình ModSecurity
