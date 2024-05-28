# First of all, thanks for this awesome nginx.conf that saved my life :)
https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/insecure/postgres/fpm/web/nginx.conf

## If you want HTTPS, please add this in config.php (nextcloud/config/config.php)
```
'overwriteprotocol' => 'https'
```

## If you want to use custom domain, please add this in config.php (nextcloud/config/config.php)
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
https://hub.docker.com/_/nextcloud/tags
https://hub.docker.com/_/postgres/tags