## SNMP

Simple Network Management Protocol (SNMP)
- network management 
- based on UDP
- port 161
- many hosts use "public" read-only strings sometimes need to be guessed
- Three versions SNMPv1, SNMPv2c, SNMPv3 , Version 1 and 2c have no encryption

- Can also be installed on linux
### SNMP Enumeration

#### Nmap
needs sudo

```sh
nmap --script smnp-win32-users -p 161 <target-ip> #enumarate users on that machine
```

#### onesixtyone
can enumerate community strings

```sh
onesixtyone -c /usr/share/doc/onesixtyone/dic.txt <target-ip>
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
```

### Exploit

#### on linux if readable and writeable
there is an metasploit module for that
```sh
#This info is preliminary not tested
msfconsole
auxiliary(scanner/snmp/snmp_set)
```