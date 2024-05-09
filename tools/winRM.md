# WinRM
- ports 5985, 5986

## Usage
```shell
-p password
-u username 
-i ip address

evil-winrm -i 10.129.152.215 -u administrator -p badminton
```
## Footprinting

### Nmap
```shell
nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n
```

