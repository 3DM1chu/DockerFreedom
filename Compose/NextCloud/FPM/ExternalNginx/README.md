## App is Working Under Port 9000

## First of all, Thanks for this Awesome nginx.conf That Saved My Life 😊
[nginx.conf](https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/insecure/postgres/fpm/web/nginx.conf)

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

### Useful Links for Docker:
- Nextcloud Docker Images: [Nextcloud Tags](https://hub.docker.com/_/nextcloud/tags)
- PostgreSQL Docker Images: [PostgreSQL Tags](https://hub.docker.com/_/postgres/tags)
