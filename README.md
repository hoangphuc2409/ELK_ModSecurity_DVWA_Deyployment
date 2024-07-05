# ELK stack + ModSecurity + DVWA Lab
## Tổng quan
## Topology
## Triển khai
### 1. Cài đặt DVWA
#### Tạo DVWA Apache website
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
![image](https://github.com/hoangphuc2409/ELK_ModSecurity_DVWA_Deyployment/assets/130757038/a57a3142-820a-4c57-a043-1f30bb6160a8)
### 2. Cấu hình ModSecurity
