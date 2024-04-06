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
- know your tools
- Tools are good but manuel also
- use robots.txt , look at the sensitive directories/files
- view page sources
- turn on developer tools in browser
- look at cookies 
  - PHPSESSID = PHP
  - ASPSESSID = ASP
- look at network tab
- look with curl maybe you see something you dont saw before
- 