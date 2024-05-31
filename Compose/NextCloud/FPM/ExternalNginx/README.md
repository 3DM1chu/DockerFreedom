App is working under port 9000

## First of all, thanks for this awesome nginx.conf that saved my life :)
https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/insecure/postgres/fpm/web/nginx.conf

### If you want HTTPS, please add this in config.php
> nextcloud/config/config.php
```
'overwriteprotocol' => 'https'
```

### If you have problems with not seeing DB while initialization, please add this in config.php
> nextcloud/config/config.php
```
  'dbtype' => 'pgsql',
  'dbname' => 'nextcloud',
  'dbhost' => 'NAME_OF_YOUR_DOCKER_POSTGRES_DB_CONTAINER_NAME',
  'dbuser' => 'nextcloud',
  'dbpassword' => 'DB_PASSWORD_PLEASE_CHANGE'
```

### If you want to use custom domain, please add this in config.php
> nextcloud/config/config.php
```
...
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => 'server1.example.com',
   2 => '192.168.1.50',
   3 => '[fe80::1:50]',
),
...
```

> Please use only DNS name, without http / https, like: server1.example.com


### Useful links for docker:
https://hub.docker.com/_/nextcloud/tags \
https://hub.docker.com/_/postgres/tags 