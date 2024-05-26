# CrackMapExec
- Docu: https://web.archive.org/web/20231116172005/https://www.crackmapexec.wiki/
- Repo https://github.com/byt3bl33d3r/CrackMapExec
## Installation
```bash
sudo apt-get -y install crackmapexec
```

## Usage
```bash
crackmapexec -h #help
crackmapexec smb -h #help for smb

crackmapexec <proto> <target-IP> -u <user or userlist> -p <password or passwordlist>
crackmapexec winrm 10.129.42.197 -u user.list -p password.list 
# example with target to crack winrm


```
