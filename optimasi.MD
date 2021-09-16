### Optimasi Ngix
```bash
nano /etc/nginx/nginx.conf
```
ini tidak perlu menambah baris, tetapi cukup dengan meyamakan script seperti dibawah ini:
```bash
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 7680;
	multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	##
	# Gzip Settings
	##

	gzip on;

	gzip_vary on;
	gzip_proxied any;
	gzip_comp_level 6;
	gzip_buffers 16 8k;
	gzip_http_version 1.1;
	gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}
```
selanjutnya restart nginx: 
```bash
systemctl restart nginx.service
```
kemudian lanjutkan dgn optimasi PHP FPM.

### Optimasi PHP-FPM
jgn ditambah barisnya, cukup ubah opsi yang pada file `www.conf`
yang perlu diubah adalah pada bagian `pm.max_children` ke bawah. 
```bash
nano /etc/php/7.4/fpm/pool.d/www.conf
```

```bash
[www]
user = www-data
group = www-data
listen = /run/php/php7.4-fpm.sock

listen.owner = www-data
listen.group = www-data

pm = dynamic
pm.max_children = 500
pm.start_servers = 20
pm.min_spare_servers = 10
pm.max_spare_servers = 500

security.limit_extensions = .php
```
Selanjutnya restart php-fpm:
```bash
systemctl restart php-fpm.service
```
kemudian lanjutkan dgn optimasi database server `mariadb`

#Optimasi database server
```bash
nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
pada bagian `[mysqld]` dibawahnya finetunning carilah max_connections dan ubah value menjadi 500 
dan juga tambahkan baris dibawah ini dibawahnya `innodb_large_prefix = ON`
```bash
innodb_buffer_pool_size	= 1024M
innodb_log_buffer_size	= 256M
```
