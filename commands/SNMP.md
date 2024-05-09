## SNMP

Simple Network Management Protocol (SNMP)
- network management 
- based on UDP
- port 161
- port 162 for traps
- many hosts use "public" read-only strings sometimes need to be guessed
- Three versions SNMPv1, SNMPv2c, SNMPv3 , Version 1 and 2c have no encryption
- Can also be installed on linux


### Configuration
#### SNMP Daemon Config
```sh


cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'

sysLocation    Sitting on the Dock of the Bay
sysContact     Me <me@example.org>
sysServices    72
master  agentx
agentaddress  127.0.0.1,[::1]
view   systemonly  included   .1.3.6.1.2.1.1
view   systemonly  included   .1.3.6.1.2.1.25.1
rocommunity  public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly

```
### Dangerous Settings
| Setting                           | Description                                                                 |
|-----------------------------------|-----------------------------------------------------------------------------|
| rwuser noauth                     | Provides access to the full OID tree without authentication.                |
| rwcommunity `<community string>` `<IPv4 address>` | Provides access to the full OID tree regardless of where the requests were sent from. |
| rwcommunity6 `<community string>` `<IPv6 address>` | Same access as with rwcommunity, with the difference of using IPv6.         |


### SNMP Enumeration

#### Nmap
needs sudo

```sh
sudo nmap --script snmp-win32-users -p 161 10.129.95.111 #enumarate users on that machine
sudo nmap -sC -sV -p 161 10.129.95.111 #enumarate users on that machine
```

#### onesixtyone
- can enumerate community strings
```sh
sudo apt install onesixtyone
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt 10.129.67.141
```

#### braa
- Once we know a community string, we can use it with braa to brute-force the individual OIDs and enumerate the information behind them.

```sh
sudo apt install braa
braa <community string>@<IP>:.1.3.6.*   # Syntax
braa public@10.129.14.128:.1.3.6.*
```

#### SMNP Check & SMNP Walk
1.) is Cleaner:
```sh
snmp-check <target-ip> 
```
2.)
```sh   
snmpwalk -c public -v1 <target-ip> <OID-String> 
#The OID in the snmpwalk command stands for Object Identifier. 
# It's a unique identifier used to represent a specific object in the Management Information Base (MIB) hierarchy in SNMP (Simple Network Management Protocol).
#For example, an OID string might look like this: 1.3.6.1.2.1.1, 
# where each number represents a level in the MIB hierarchy.

snmpwalk -v2c -c public 10.129.95.111
# In the case of a misconfiguration, we would get approximately the same results from snmpwalk as just shown above. Once we know the community string
# and the SNMP service that does not require authentication (versions 1, 2c), we can query internal system information like in the previous example.
```

### Exploit

#### on linux if readable and writeable
there is an metasploit module for that
```sh
#This info is preliminary not tested
msfconsole
auxiliary(scanner/snmp/snmp_set)
```