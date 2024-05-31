## If you have problems with desktop sync, check this youtube video
https://www.youtube.com/watch?v=iFHbzWhKfuU&t=570s

## How to run migration to other database system like from SQLite to PostGreSQL
1. Connect to nextcloud container (the one with /var/www/html)
2. Login as www-data (might be needed custom shell to start with) (its included inside this code :))
2a. For PostGreSQL:
```
su -l www-data -s /bin/bash \
cd /var/www/html \
php occ db:convert-type --all-apps --password="DB_PASSWORD" pgsql DB_USER DOCKER_DB_CONTAINER_NAME DB_NAME
```
2b. For MySQL:
```
TODO :)
```
> Replace DOCKER_DB_CONTAINER_NAME with appropiate name (use DNS names instead of network IPs if you don't have them static, you can later change them in config.php (dbhost) if you messed up :)) like me haha