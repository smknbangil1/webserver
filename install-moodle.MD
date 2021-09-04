### Instalasi Moodle
#### untuk menginstall moodle kita harus mengaktifkan beberapa konfigurasi dasar berikut ini
```baah
nano /etc/php/7.4/fpm/php.ini
```
caria opsi ini tiap baris, dan buat seperti berikut:
```bash
file_uploads = On
allow_url_fopen = On
short_open_tag = On
memory_limit = 256M
cgi.fix_pathinfo = 0
upload_max_filesize = 100M
max_execution_time = 360
date.timezone = Asia/Jakarta
```
simpan
#### lalu restart php dan pastikan tidak mendapatkan error :)
```bash
systemctl restart php7.4-fpm.service
```
### Next... membuat file database untuk moodle
```bash
mysql
```
```bash
CREATE DATABASE moodledb;
```
```bash
#### membuat user database
CREATE USER 'samson'@'localhost' IDENTIFIED BY 'myDBpassword';
```
contoh diatas saya buat user database dgn nama somson, anda bisa ganti dengan username lainnya sesuai selera anda :)
#### memberi hak akses samson terhadap file moodledb
```bash
GRANT ALL ON moodledb.* TO 'samson'@'localhost' WITH GRANT OPTION;
```
#### simpan dan keluar dari operasi database
```bash
FLUSH PRIVILEGES;
```
```bash
EXIT;
```

config vhost untuk domain atau sub domain
```bash
server {
    listen 80;
    listen [::]:80;
    root /var/www/moodle;
    index  index.php index.html index.htm;
    server_name  example.com;

    client_max_body_size 100M;
    autoindex off;
    location / {
        try_files $uri $uri/ =404;
    }

    location /dataroot/ {
      internal;
      alias /var/www/moodledata/;
    }

    location ~ [^/].php(/|$) {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
