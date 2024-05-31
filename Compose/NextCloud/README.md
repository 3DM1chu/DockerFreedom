## How to Run Migration to Other Database System (e.g., from SQLite to PostGreSQL)

### Step 1: Connect to Nextcloud Container
1. Connect to the Nextcloud container, specifically the one containing `/var/www/html`.

### Step 2: Login as `www-data`
2. Login as the `www-data` user. You might need a custom shell to start with. (This is included inside the code.)

#### For PostGreSQL:

```bash
su -l www-data -s /bin/bash
cd /var/www/html
php occ db:convert-type --all-apps --password="DB_PASSWORD" pgsql DB_USER DOCKER_DB_CONTAINER_NAME DB_NAME
```

Replace:
- `DB_PASSWORD`: Your PostGreSQL database password.
- `DB_USER`: Your PostGreSQL database username.
- `DOCKER_DB_CONTAINER_NAME`: The name of your Docker container running the PostGreSQL database.
- `DB_NAME`: The name of your PostGreSQL database.

#### For MySQL:
```
TODO :)
```

> **Note:** Replace `DOCKER_DB_CONTAINER_NAME` with the appropriate name. If you don't have static DNS names, you can use network IPs instead. Later, you can change them in `config.php` (dbhost) if needed.

---

For troubleshooting or further assistance, you can refer to [this YouTube video](https://www.youtube.com/watch?v=iFHbzWhKfuU&t=570s) if you encounter any issues with desktop sync.

Feel free to reach out if you have any questions or need additional support!