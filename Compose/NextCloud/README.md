### How to Run Migration to Other Database System (e.g., from SQLite to PostGreSQL)

#### Step 1: Connect to Nextcloud Container
1. Connect to the Nextcloud container, specifically the one containing `/var/www/html`.

#### Step 2: Login as `www-data`
2. Login as the `www-data` user. You might need a custom shell to start with. (This is included inside the code.)

#### > For PostGreSQL:

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


---

For troubleshooting or further assistance, you can refer to [this YouTube video](https://www.youtube.com/watch?v=iFHbzWhKfuU&t=570s) if you encounter any issues with desktop sync.

Feel free to reach out if you have any questions or need additional support!