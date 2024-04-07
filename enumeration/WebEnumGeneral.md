## Web Enumeration
Test everything

### Scanner
- nikto
- nmap
```sh
nmap --vuln # can also find possible SQL Injections and CSRF vulnerabilities 
```

### Directory Bruteforcing
find hidden directories, paths and files
- gobuster
- dirb
- dirbuster

### Proxies
- Burp Suite
- Cyberchef
- OWASP ZAP

### Manual Enumeration
- check for robots.txt , look at the sensitive directories/files
- view page sources
- turn on developer tools in browser
- look at cookies 
  - PHPSESSID = PHP
  - ASPSESSID = ASP
- look at network tab
- look with curl maybe you see something you dont saw before


### CMS's
- Check for version
- Check for known Exploits
- check robots.txt to get infos
- Try standard passwords and usernames
- Try to check if /phpmyadmin

#### Attack path
- enumarate
- try to authenticate with standard usernames and passwords
- try to enumerate the underlying system and database
- if you are on dashboard you can often add code
- if you are in check the database if possible
- 
