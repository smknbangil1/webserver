### cara install SSL Lets Encript di server ubuntu
masuk sebagai root dengan cara `sudo su` kemudian masukin passwordnya, 
kemudian ketik command dibawah ini:
```bash 
apt-get update -y
```
```bash 
apt-get install snapd -y
```
```bash
snap install core; snap refresh core
```
lalu install cerbot
```bash
snap install --classic certbot
```
membuat symlink cerbot 
```bash
ln -s /snap/bin/certbot /usr/bin/certbot
```
Jalankan perintah ini untuk mendapatkan sertifikat dan minta Certbot mengedit konfigurasi VHOST Nginx Anda secara otomatis untuk melayaninya:
```bash
certbot --nginx
```
kalau ada persetujuan Term of Service jawab dengan A (agree), atau Y(yes), dah ini tinggal ikuti aja dialog yg ditampilkan. 
#
kalau ada kesulitan bisa chat ke wa dan screenshot ya mas :)
Selesai. Terima kasih
