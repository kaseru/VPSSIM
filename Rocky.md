## Nếu bị lỗi ko start đc nginx 
Mở file /etc/nginx/nginx.conf. Comment lại dòng này nếu log lỗi do dòng này
```# load_module modules/ngx_http_geoip_module.so;```

# Nếu đã start đc nginx nhưng ko truy cập đc
- Check csf 
```sudo csf -v```

- Nếu chưa có thì cài đặt
```
# Cài đặt các gói cần thiết để CSF hoạt động:
sudo yum install wget perl-libwww-perl.noarch perl-LWP-Protocol-https perl-GDGraph -y
cd /usr/src
sudo wget https://download.configserver.com/csf.tgz
sudo tar -xvzf csf.tgz
cd csf
sudo sh install.sh
```

- Kiểm tra xem CSF được cài đặt đúng cách
```sudo perl /usr/local/csf/bin/csftest.pl
```


- Nếu chưa có perl => Cài đặt
```
sudo yum install perl-CPAN -y
sudo cpan
```

- Khởi động csf và ldd cùng hệ thống
```
sudo systemctl enable csf
sudo systemctl enable lfd
```

- Lưu ý ldd chỉ hoạt động khi csf testing đc tắt
```
vim /etc/csf/csf.conf
```
