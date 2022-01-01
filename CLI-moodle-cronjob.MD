```bash
$ crontab -u www-data -e
```
masukkan ini:
```bash
* * * * * /usr/bin/php /var/www/moodle/admin/cli/cron.php >/dev/null 2>&1
```
