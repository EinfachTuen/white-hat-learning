## How to get inside:

### Web Edition:

1.) run Nmap on server

2.) when http found try to open website

2a.) Websites redirect, this can be named based virtual hosting

2a1.) add the ip to /etc/hosts

3.) run gobuster with a suifficient wordlist to find hidden directories

3a.) If a url parameter is found, try to inject a file

4.) if login is present try standard credentials:

```
    admin:admin
    guest:guest
    user:user
    root:root
    administrator:password
```

5.) try sql injection