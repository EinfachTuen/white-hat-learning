## Nikto
Robust web server scanner that checks for over 6700 potentially dangerous files/programs, checks for outdated versions of over 1250 servers, and version specific problems on over 270 servers. It also checks for server configuration items such as the presence of multiple index files, HTTP server options, and will attempt to identify installed software and web servers. Scan items and plugins are frequently updated and can be automatically updated
- makes a ton of requests
- gives a lot of infos
- can be false positive
- can be noisy

### Use
```sh
nikto -h 10.129.20.215 -p 80 #scan a target
```
