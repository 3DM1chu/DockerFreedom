# First of all, thanks for this awesome nginx.conf that saved my life :)
https://github.com/nextcloud/docker/blob/master/.examples/docker-compose/insecure/postgres/fpm/web/nginx.conf

## If you want HTTPS, please add this to config.php inside config folder (nextcloud)
'overwriteprotocol' => 'https'

## If you want to use custom domain, please add it in config.php inside config folder (nextcloud)
```
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => 'server1.example.com',
   2 => '192.168.1.50',
   3 => '[fe80::1:50]',
),
```

> Please use only DNS name, without http / https, like: server1.example.com