# WinRM
- https://learn.microsoft.com/en-us/windows/win32/winrm/portal
- ports 5985, 5986

## Usage
```shell
evil-winrm -i 10.129.152.215 -u administrator -p badminton
# -p password
# -u username 
# -i ip address
```

## Footprinting
### Nmap
```shell
nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n
```

## Crack Password
- more details at crackmapexec.md
```shell
crackmapexec winrm 10.129.42.197 -u user.list -p password.list 
```


