# Install Web Server di Ubuntu 20.04

## periksa seluruh interface NIC
```bash
ifconfig -a
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
        search: []
  version: 2
```

### Ubah Hostname di Ubuntu
```bash
hostnamectl set-hostname docker-node1
```
### Ubah timezone WIB
```bash
timedatectl set-timezone Asia/Jakarta
```
### ===================
