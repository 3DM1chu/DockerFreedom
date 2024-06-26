# If DNS not working like EAI errors showing up in logs then do this:
### Create resolv.conf (not container) and put nameserver 8.8.8.8
> remember to mount it inside container to /etc/resolv.conf

# If you want to use Reverse Proxy
Please remember to enable WebSockets :)