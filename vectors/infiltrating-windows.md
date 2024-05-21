# Infiltrating Windows
Table of known Windows vulnerabilities:
- https://www.cvedetails.com/vendor/26/Microsoft.html

## Prominent Windows Exploits
- print nightmare details: https://0xdf.gitlab.io/2021/07/08/playing-with-printnightmare.html

| Vulnerability  | Description |
|----------------|-------------|
| MS08-067       | MS08-067 was a critical patch pushed out to many different Windows revisions due to an SMB flaw. This flaw made it extremely easy to infiltrate a Windows host. It was so efficient that the Conficker worm was using it to infect every vulnerable host it came across. Even Stuxnet took advantage of this vulnerability. |
| Eternal Blue   | MS17-010 is an exploit leaked in the Shadow Brokers dump from the NSA. This exploit was most notably used in the WannaCry ransomware and NotPetya cyber attacks. This attack took advantage of a flaw in the SMB v1 protocol allowing for code execution. EternalBlue is believed to have infected upwards of 200,000 hosts just in 2017 and is still a common way to find access into a vulnerable Windows host. |
| PrintNightmare | A remote code execution vulnerability in the Windows Print Spooler. With valid credentials for that host or a low privilege shell, you can install a printer, add a driver that runs for you, and grants you system-level access to the host. This vulnerability has been ravaging companies through 2021. 0xdf wrote an awesome post on it here. |
| BlueKeep       | CVE 2019-0708 is a vulnerability in Microsoft's RDP protocol that allows for Remote Code Execution. This vulnerability took advantage of a miss-called channel to gain code execution, affecting every Windows revision from Windows 2000 to Server 2008 R2. |
| Sigred         | CVE 2020-1350 utilized a flaw in how DNS reads SIG resource records. It is a bit more complicated than the other exploits on this list, but if done correctly, it will give the attacker Domain Admin privileges since it will affect the domain's DNS server which is commonly the primary Domain Controller. |
| SeriousSam     | CVE 2021-36924 exploits an issue with the way Windows handles permission on the C:\Windows\system32\config folder. Before fixing the issue, non-elevated users have access to the SAM database, among other files. This is not a huge issue since the files can't be accessed while in use by the pc, but this gets dangerous when looking at volume shadow copy backups. These same privilege mistakes exist on the backup files as well, allowing an attacker to read the SAM database, dumping credentials. |
| Zerologon      | CVE 2020-1472 is a critical vulnerability that exploits a cryptographic flaw in Microsoft’s Active Directory Netlogon Remote Protocol (MS-NRPC). It allows users to log on to servers using NT LAN Manager (NTLM) and even send account changes via the protocol. The attack can be a bit complex, but it is trivial to execute since an attacker would have to make around 256 guesses at a computer account password before finding what they need. This can happen in a matter of a few seconds. |

- MS17-010 (EternalBlue)  Windows 2008 to Server 2016
## Enumerating Windows

### Ping
- Operating system can be identified by TTL
- https://davidstein.cz/2021/12/22/standard-icmp-return-ttl-values-by-os/
```shell
ping 10.129.201.97 # 
PING 192.168.86.39 (192.168.86.39): 56 data bytes
64 bytes from 192.168.86.39: icmp_seq=0 ttl=128 time=102.920 ms
64 bytes from 192.168.86.39: icmp_seq=1 ttl=128 time=9.164 ms
```

### OS Detection Scan
- this can be blocked by firewalls
```shell
sudo nmap -v -O 10.129.201.97 # OS detection scan
...
Running: Microsoft Windows 10
OS CPE: cpe:/o:microsoft:windows_10
OS details: Microsoft Windows 10 1709 - 1909
...
```

### Banner grap script on open ports
 can give good results
```shell
sudo nmap -v 10.129.201.97 --script banner.nse
```

### Determine Eternal blue vuln
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
## Windows typical File Types and how they are used in Pentesting:
### DLLs
Dynamic Linking Libraries (DLLs) are shared library files in Microsoft OS that provide reusable code and data for multiple programs. Pentesters can inject malicious DLLs or hijack vulnerable ones to elevate privileges to SYSTEM or bypass User Account Controls.

### Batch
Batch files are DOS scripts (.bat) used by system admins for task automation. Pentesters can use batch files to run commands on a host, open ports, or connect back to an attacking box, then perform enumeration and report back through the open port.

### VBS
VBScript, based on Visual Basic, is used for client-side scripting in web servers. Though dated and often disabled in modern browsers, VBS is still used in phishing attacks to execute code via user actions, like enabling Macros in an Excel document.

### MSI
.MSI files are installation databases for Windows Installer. Pentesters can craft payloads as .msi files and use msiexec to execute them on a host, granting further access like an elevated reverse shell.

### PowerShell
PowerShell is a shell environment and scripting language in Microsoft OS, based on the .NET framework. It offers extensive options for gaining shells and executing commands on a host, aiding in various penetration testing processes.


## Payload generation
| Resource                          | Description |
|-----------------------------------|-------------|
| MSFVenom & Metasploit-Framework [Source](https://github.com/rapid7/metasploit-framework) | MSF is an extremely versatile tool for any pentester's toolkit. It serves as a way to enumerate hosts, generate payloads, utilize public and custom exploits, and perform post-exploitation actions once on the host. Think of it as a Swiss Army knife. |
| Payloads All The Things [Source](https://github.com/swisskyrepo/PayloadsAllTheThings) | Here, you can find many different resources and cheat sheets for payload generation and general methodology. |
| Mythic C2 Framework [Source](https://github.com/its-a-feature/Mythic)     | The Mythic C2 framework is an alternative option to Metasploit as a Command and Control Framework and toolbox for unique payload generation. |
| Nishang [Source](https://github.com/samratashok/nishang)                | Nishang is a framework collection of Offensive PowerShell implants and scripts. It includes many utilities that can be useful to any pentester. |
| Darkarmour [Source](https://github.com/bats3c/darkarmour)              | Darkarmour is a tool to generate and utilize obfuscated binaries for use against Windows hosts. |

## Transfer Payloads
- anykind of protokoll like ftp, http etc.
- Impacket: can help for psexec, smbclient, wmi, Kerberos and smb as server
- Payload all the things has a lot of helper: psexec, smbclient, wmi, Kerberos
- Metasploit

## CMD vs Powershell
### Use CMD when:
- You are on an older host that may not include PowerShell.
- When you only require simple interactions/access to the host.
- When you plan to use simple batch files, net commands, or MS-DOS native tools.
- When you believe that execution policies may affect your ability to run scripts or other actions on the host.

### Use PowerShell when:
- You are planning to utilize cmdlets or other custom-built scripts.
- When you wish to interact with .NET objects instead of text output.
- When being stealthy is of lesser concern.
- If you are planning to interact with cloud-based services and hosts.
- If your scripts set and use Aliases.

## new Special Windows attack steahlty by WSL
- https://www.bleepingcomputer.com/news/security/new-malware-uses-windows-subsystem-for-linux-for-stealthy-attacks/