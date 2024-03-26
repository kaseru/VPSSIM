@@ -1,30 +0,0 @@
# VPSSIM

Dành cho CentOS 7
```
bash <( curl -k https://raw.githubusercontent.com/kaseru/VPSSIM/master/vpssim_fix )
```

Đây là bản Fix giúp bạn chạy được bình thường sau khi cài đặt VPSSIM ( cài đặt mới hoàn toàn ), không còn bị lỗi không chạy được PHP nữa

**Đã Test trên CentOS 7 của**

+ Amazon Lightsail
+ OVH
+ Linode
+ Vultr
+ VPS Viettel

Lưu ý: Bản cài đặt này chỉ Fix lỗitrong quá trình cài đặt, còn lại các thành phần của VPSSIM không thay đổi. Việc nhập được KEY hay không phụ thuộc vào bên vpssim.

## Cài đặt thủ công
- Copy menu.zip to ```/etc/vpssim/```
- Copy file centos7/vpssim-setup to ```/etc/vpssim/.tmp/vpssim-setup```
- Chmod ```chmod +x /etc/vpssim/.tmp/vpssim-setup ```
- Install ```bash /etc/vpssim/.tmp/vpssim-setup```


## Nếu lỗi phpmyadmin thì cài đặt bằng tay

```sh /etc/vpssim/menu/dg-fix-nang-cap-phpmyadmin ```

## Cài đặt thư viên thêm gcc++, nodejs, yarn, pm2, redis, libvips

```sh /etc/vpssim/menu/dg-install-nodejs-yarn-pm2-vips-redis ```

## Backup db sang Gooogle driver

- Chuẩn bị file config vào đường dẫn
```/root/.config/rclone/rclone.conf```

- Run backup
```sh /etc/vpssim/menu/dg-backup ```


- Fix lỗi Error: /lib64/libstdc++.so.6: version `CXXABI_1.3.9' not found
```
strings /usr/lib64/libstdc++.so.6 | grep GLIBC
strings /usr/lib64/libstdc++.so.6|grep CXXABI

if not found CXXABI_1.3.9，update libstdc++.so.6

download libstdc++.so.6.0.26 (https://cdn.frostbelt.cn/software/libstdc%2B%2B.so.6.0.26)，

copy to /usr/lib64/, and :

cd /usr/lib64/
ln -snf ./libstdc++.so.6.0.26 libstdc++.so.6

Error: /lib64/libc.so.6: version `GLIBC_2.18' not found
install GLIBC_2.18:

curl -O http://ftp.gnu.org/gnu/glibc/glibc-2.18.tar.gz
tar zxf glibc-2.18.tar.gz
cd glibc-2.18/
mkdir build
cd build/
../configure --prefix=/usr
make -j2
make install

```

- Fix lỗi mysql ko thể khởi động ```cant connect to local msql server through socket var/lib/mysql/mysql.sock```

Chạy lệnh
```mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql ```

Sau đó start
```systemctl start mariadb```

Chạy khi khơi động
```systemctl enable mariadb```
