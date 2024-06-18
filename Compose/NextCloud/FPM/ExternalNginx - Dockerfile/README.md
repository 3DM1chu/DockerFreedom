## App is Working Under Port 9000

## First of all, Thanks for this Awesome nginx.conf That Saved My Life 😊
[nginx.conf](https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/insecure/postgres/fpm/web/nginx.conf)

## This version includes Dockerfile so you can for example install external storage app (installs smbclient)
To install app:
```bash
docker exec -it DOCKER_CONTAINER_ID -u 33 /bin/bash
php occ app:enable APP_NAME
```
> -u 33 -> to sign as www-data, APP_NAME can be fe: files_external

### If You Want HTTPS, Please Add This in config.php
> `var/www/html/config/config.php` or `NEXTCLOUD_MOUNT_PATH_TO_VAR_WWW_HTML/config/config.php`

```php
'overwriteprotocol' => 'https'
```

### If You Have Problems with Not Seeing DB While Initialization, Please Add This in config.php
> `var/www/html/config/config.php` or `NEXTCLOUD_MOUNT_PATH_TO_VAR_WWW_HTML/config/config.php`

```php
'dbtype' => 'pgsql',
'dbname' => 'nextcloud',
'dbhost' => 'NAME_OF_YOUR_DOCKER_POSTGRES_DB_CONTAINER_NAME',
'dbuser' => 'nextcloud',
'dbpassword' => 'DB_PASSWORD_PLEASE_CHANGE'
```

### If You Want to Use Custom Domain, Please Add This in config.php
> `var/www/html/config/config.php` or `NEXTCLOUD_MOUNT_PATH_TO_VAR_WWW_HTML/config/config.php`

```php
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => 'server1.example.com',
   2 => '192.168.1.50',
   3 => '[fe80::1:50]',
),
```

> **Note:** Please use only DNS names without http/https, like: server1.example.com

### How to Run Migration to Other Database System (e.g., from SQLite to PostGreSQL)

Step 1. Connect to the Nextcloud container (probably named 'app'), specifically the one containing `/var/www/html`

Step 2: Login as `www-data` user
```bash
su -l www-data -s /bin/bash
```

#### > For PostGreSQL:

```bash
cd /var/www/html
php occ db:convert-type --all-apps --password="DB_PASSWORD" pgsql DB_USER DOCKER_DB_CONTAINER_NAME DB_NAME
```

Replace:
- `DB_PASSWORD`: Your PostGreSQL database password.
- `DB_USER`: Your PostGreSQL database username.
- `DOCKER_DB_CONTAINER_NAME`: The name of your Docker container running the PostGreSQL database.
- `DB_NAME`: The name of your PostGreSQL database.

#### > For MySQL:
```
TODO :)
```

> **Note:** Replace `DOCKER_DB_CONTAINER_NAME` with the appropriate name. If you don't have static DNS names, you can use network IPs instead. Later, you can change them in `config.php` (dbhost) if needed.

---

### < Quick Tips >

#### > Correct File Permissions

**Owner and Group:** `www-data`

> **Inside /var/www/html:**
- Directories: `rwxr-xr-x` (755) 
  - **Exception:** `data` directory: `rwxrwx---` (770)
- Files: `rw-r--r--` (644)
  - **Exceptions:** `.htaccess` and `.user.ini`: `rwxrwxr-x` (775)

> **Inside config folder:**
- Files: `rw-r--r--` (644)
  - **Exception:** `config.php`: `rw-r-----` (640)

> **Inside data folder:**
- Directories: `rwxrwxr-x` (775)
- Files: `rw-r-----` (640)
  - **Exceptions:**
    - `.htaccess` and `index.html`: `rw-r--r--` (644)
	- `.ocdata` and `owncloud.db`: `rwxrwxr-x` (775)

> **Inside apps folder:**
- Directories: `rwxr-xr-x` (755)
- Files: `rw-r--r--` (644)

#### > If you want to increase timeout for uploads (for big files)
Step 1: Put it inside server { ... } in nginx.conf
```
# set max upload size and increase upload timeout:
client_max_body_size 200G;
client_body_timeout 86400s;
fastcgi_buffers 64 4K;
```

Step 2: Inside 'location ~ \.php(?:$|/) {' put
```
fastcgi_request_buffering off;
fastcgi_read_timeout 86400s;
proxy_read_timeout 3600s;
fastcgi_max_temp_file_size 0;
```

Useful command for restarting nginx if needed (inside nginx container):
```bash
nginx -s reload
```

### Useful Links for Docker:
- Nextcloud Docker Images: [Nextcloud Tags](https://hub.docker.com/_/nextcloud/tags)
- PostgreSQL Docker Images: [PostgreSQL Tags](https://hub.docker.com/_/postgres/tags)
