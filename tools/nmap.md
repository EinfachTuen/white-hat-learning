## Nmap Network Enumeration

### Tipps
- Dont asume ports for same services are always same
- Always check for all ports
- Try to enumerate service type and version
- if not enought information try ncat and other tools

### Single IP
```sh
nmap 192.169.1.1 
```
### Multiple IP
```sh
nmap 192.169.1.1/24
nmap 192.169.1.1-100
```

### Targets from files
```sh
nmap -iL targets.txt #ip list
```

### Specific ports
```sh
-p 80,443,8080 # or range of ports
-p- # all ports
```

### Parameters
```sh
nmap <scan types> <options> <target>

SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM #TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU #UDP Scan
  -sN/sF/sX #TCP Null, FIN, and Xmas scans
  --scanflags <flags> # Customize TCP scan flags
  -sI <zombie host[:probeport]> # Idle scan
  -sY/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO #IP protocol scan
  -b <FTP relay host> # FTP bounce scan
  -v #Increase verbosity level (use -vv or more for greater effect) -vvv the most verbosity
  -sV #switch stands for version detection
  --min-rate=1000 #This is used to specify the minimum number of packets that Nmap should send per second; it speeds up the scan as the number goes higher
  -sC #run with default Scripts (more Infos)
  -Pn #Treat all hosts as online -- skip host discovery
```
If the target sends an SYN-ACK flagged packet back to the scanned port, Nmap detects that the port is open.
If the packet receives an RST flag, it is an indicator that the port is closed.
If Nmap does not receive a packet back, it will display it as filtered. Depending on the firewall configuration, 
certain packets may be dropped or ignored by the firewall.

### Find General Infos about ports:
Find informations about ports:
https://www.speedguide.net/port.php?port=3389

### UDP Scan
```sh
nmap -sU 192.169.1.1
```
### Treat all hosts as online / No Ping
```sh
nmap -Pn 192.169.1.1
```
### Send Output to a file:
```sh
nmap -oN output.txt # normal
nmap -oX output.xml # xml
nmap -oG output.grep # grepable
nmap -oA output # all formats at once
```

### Timing
```sh
nmap -T0 # Paranoid
nmap -T1 # Sneaky
nmap -T2 # Polite
nmap -T3 # Normal
nmap -T4 # Aggressive
nmap -T5 # Insane
```
### Use Scan for Vulnarabilities
```sh
nmap --script vuln # goes trough default vulnarabe scripts
```
### Aggressive Scan
```sh
nmap -A # Aggressive scan like -sV -sC but more aggressive better not in production
```

### SMB Scan
```sh
nmap <target> --script smb-enum* # Enumerates SMB shares on Windows and Linux systems.
nmap <target> --script smb-vuln* # Check for Vulnerabilities on SMB
nmap <target> --script smb-os* # Check for OS on SMB

* # wildcard for several scripts
```
### Example Uses in Hack The Box
#### Usual scripts:
```sh
nmap -p- -sV -sC --min-rate=100000 10.129.142.225
```

```sh
nmap -p- -sV -sC -Pn --min-rate=100000 10.129.251.52
```

#### Special scripts:

```sh
# at first scan without details and than scan with:
ports=$(nmap -p- --min-rate=1000 -T4 10.129.230.220 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//) nmap -p$ports -sV -sC 10.129.230.220
```
