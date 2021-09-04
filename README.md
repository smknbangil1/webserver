# Install Web Server di Ubuntu 20.04

## periksa seluruh interface NIC
```bash
ip a
```

## konfig LAN
```bash
nano /etc/netplan/00-installer-config.yaml
```
### terus masukin syntax yaml sesuai kebutuhan dan topologi di sekolah
contoh di jaringan saya, berikut ini
```yaml
network:
  ethernets:
    ens18:
      addresses:
      - 10.10.10.10/24
      gateway4: 10.10.10.1
      nameservers:
        addresses:
        - 8.8.4.4
        - 8.8.8.8
        search: [google.com]
  version: 2
```

### Ubah Hostname di Ubuntu
```bash
hostnamectl set-hostname myserver
```
### Ubah timezone WIB
```bash
timedatectl set-timezone Asia/Jakarta
```
### install web-server nginx
```bash
apt-get install nginx -y
``````

#### cek web server apakah sudah terinstall dengan baik, dibuktikan bisa restart service nginx-nya
```bash
systemctl restart nginx.service
systemctl enable nginx.service
```

#### buka http://ipserver

### install package/software PHP-FPM
```bash
apt-get install php7.4-fpm -y
```

#### cek php apakah sudah terinstall dengan baik, dibuktikan bisa restart service php-nya
```bash
systemctl restart php7.4-fpm.service
systemctl enable php7.4-fpm.service
```

### install php-extension
```bash
apt-get install php7.4-common php7.4-mysql php7.4-gmp php7.4-curl php7.4-intl php7.4-mbstring php7.4-soap php7.4-xmlrpc php7.4-gd php7.4-xml php7.4-cli php7.4-zip php7.4-pspell php7.4-gd php7.4-ldap -y
```
```bash
systemctl restart php7.4-fpm.service
```

### install beberapa software pendukung lain-nya
```bash
apt-get install poppler-utils python3.8 graphviz aspell ghostscript clamav -y
```

### install package/software database
```bash
apt-get install mariadb-server mariadb-client -y
```
#### cek mariaDB apakah sudah terinstall dengan baik, dibuktikan bisa restart service mariaDB-nya
```bash
systemctl restart mariadb.service
systemctl enable mariadb.service
```

#### membuat password root/administrator database
```
mysql_secure_installation
```bash
    Enter current password for root (enter for none): silakan tekan Enter
    Set root password? [Y/n]: tekan Y
    New password: masukkan password
    Re-enter new password: Repeat password
    Remove anonymous users? [Y/n]: tekan Y
    Disallow root login remotely? [Y/n]: tekan Y
    Remove test database and access to it? [Y/n]:  tekan Y
    Reload privilege tables now? [Y/n]:  tekan Y
```
#### menguji password root database
```bash
mysql -u root -p
```
coba masukkan password yg tadi udah dibuat, pastikan bisa muncul:
```bash
MariaDB [(none)]>
```
