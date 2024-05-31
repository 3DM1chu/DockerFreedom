# DockerFreedom
I post here my A W E S O M E docker ready things :) (so i don't cry all the time :))))

## Docker useful commands
### === Logs ===

#### Attach to docker-compose logging ( must be in folder of docker-compose )
```
docker-compose logs -f
```

#### Print log files size for all containers
```
for container in $(docker ps -qa); do
    log_path=$(docker inspect --format='{{.LogPath}}' $container)
    container_name=$(docker inspect --format='{{.Name}}' $container | sed 's/\///')
    du -ch $log_path --exclude='total' | sed "s#$log_path#$container_name#g" | grep -v 'total'
done | sort -h
```

#### Delete old logs and leave only N lines with tail
```
find /var/lib/docker/containers/ -name "*-json.log" -exec sh -c 'for log; do tail -n 10000 "$log" > "$log.tmp" && mv "$log.tmp" "$log"; done' sh {} +
```
> This commands leaves 10000 lines (argument of command tail: -n 10000)