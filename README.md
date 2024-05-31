# DockerFreedom
Welcome to DockerFreedom! Here, I share my awesome Docker-ready tips and tricks to make your containerization journey smoother. No more Docker frustrations! 😄

## Docker Tips
1. You don't need to use the entire container ID to identify a container.

## < Docker Useful Commands >

### Executing on Containers

#### Log in to Interactive Mode with /bin/bash or /bin/sh
```bash
docker exec -it CONTAINER_ID /bin/bash
```
> **Note:** You can also use the full container name.

**Description:** This command allows you to access a running container's interactive shell. Replace `CONTAINER_ID` with the ID or name of your container.

### Logs

#### Attach to Docker Compose Logging
```bash
docker-compose logs -f
```
> **Note:** Must be in the folder with the `docker-compose.yml` file.

**Description:** This command attaches to the logs of all services defined in your `docker-compose.yml` file and continuously displays new log entries.

#### Print Log File Sizes for All Containers
```bash
for container in $(docker ps -qa); do
    log_path=$(docker inspect --format='{{.LogPath}}' $container)
    container_name=$(docker inspect --format='{{.Name}}' $container | sed 's/\///')
    du -ch $log_path --exclude='total' | sed "s#$log_path#$container_name#g" | grep -v 'total'
done | sort -h
```

**Description:** This script iterates through all running containers, retrieves the log file paths and sizes, and prints the size of each log file sorted by size.

- `docker ps -qa`: Lists all container IDs.
- `docker inspect --format='{{.LogPath}}' $container`: Retrieves the log file path for each container.
- `du -ch $log_path --exclude='total'`: Prints the size of the log file, excluding the total.
- `sort -h`: Sorts the log file sizes in human-readable format.

#### Delete Old Logs and Retain Only N Lines with Tail
```bash
find /var/lib/docker/containers/ -name "*-json.log" -exec sh -c 'for log; do tail -n 10000 "$log" > "$log.tmp" && mv "$log.tmp" "$log"; done' sh {} +
```
> **Note:** This command retains the last 10,000 lines (tail -n 10000).

**Description:** This command finds all Docker JSON log files, trims each log file to retain only the last 10,000 lines, and then replaces the original log file with the trimmed version.

- `find /var/lib/docker/containers/ -name "*-json.log"`: Finds all JSON log files in the Docker containers directory.
- `tail -n 10000 "$log" > "$log.tmp"`: Retains the last 10,000 lines of each log file.
- `mv "$log.tmp" "$log"`: Replaces the original log file with the trimmed version.

---

Feel free to share your thoughts and any additional tips you might have. Happy Dockering! 🚀