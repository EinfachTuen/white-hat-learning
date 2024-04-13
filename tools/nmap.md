## Nmap Network Enumeration

### Tipps
- Dont asume ports for same services are always same
- Always check for all ports
- Try to enumerate service type and version
- if not enought information try ncat and other tools
- https://nmap.org/book/host-discovery-strategies.html
### Single IP
```sh
nmap 192.169.1.1 
```
### Multiple IP
```sh
nmap 192.169.1.1/24
nmap 192.169.1.1-100
```
### Scan Network Range
```sh
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
-sn  # no port scan
-oA tnet # 	Stores the results in all formats starting with the name 'tnet'.
```
#### Scan IP List
```sh
cat hosts.lst
sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
-iL #Performs defined scans against targets in provided 'hosts.lst' list.
```

#### scan some ips
```sh
sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20| grep for | cut -d" " -f5
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
  -PE #Performs the ping scan by using 'ICMP Echo requests' against the target.
  -iL #Performs defined scans against targets in provided 'hosts.lst' list.
  -sn  # no port scan
  -oA file # 	Stores the results in all formats starting with the name 'file'.
  --reason #Displays the reason for specific result.
  --packet-trace #Shows all packets sent and received
  --disable-arp-ping
  --stats-every=5s #Shows the statistics of the scan every 5 seconds
  -F	#Scans top 100 ports.
  --initial-rtt-timeout 50ms # 	Sets the specified time value as initial RTT timeout.
  --max-rtt-timeout 100ms #Sets the specified time value as maximum RTT timeout.
  --max-retries 0 #Sets the number of retries that will be performed during the scan.
  --min-rate 300 #Sets the minimum number of packets to be sent per second.
  -sA Performs ACK scan on specified ports.
  -sS Performs SYN scan on specified ports.
  --source-port 53	Performs the scans from specified source port.
  -n	Disables DNS resolution.
  -O #Detects the operating system of the target.
  -e tun0	Sends all requests through the specified interface.
  -D RND:5	Generates five random IP addresses that indicates the source IP the connection comes from.
  -sSU #Performs SYN and UDP scans. This was helping to get Version of DNS in one HackThe Box test
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


### Timing
When Nmap sends a packet, it takes some time (Round-Trip-Time - RTT) to receive a response from the scanned port. Generally, Nmap starts with a high timeout (--min-RTT-timeout) of 100ms. Let us look at an example by scanning the whole network with 256 hosts, including the top 100 ports.
```sh
nmap -T0 # Paranoid
nmap -T1 # Sneaky 
nmap -T2 # Poli-T2
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
nmap -p- -sV -sC --min-rate=100000 10.129.142.225 --stats-every=20s -vvv -oN report
```

```sh
nmap -p- -sV -sC -Pn --min-rate=100000 10.129.251.52
```

#### Special scripts:

```sh
# at first scan without details and than scan with:
ports=$(nmap -p- --min-rate=1000 -T4 10.129.230.220 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//) nmap -p$ports -sV -sC 10.129.230.220
```

## Discovering open TCP Ports
| State |	Description |
|-------| -------- |
| open  |	This indicates that the connection to the scanned port has been established. These connections can be TCP connections, UDP datagrams as well as SCTP associations.|
|closed|	When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an RST flag. This scanning method can also be used to determine if our target is alive or not.|
|filtered|	Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.|
|unfiltered|	This state of a port only occurs during the TCP-ACK scan and means that the port is accessible, but it cannot be determined whether it is open or closed.|
|openfiltered|	If we do not get a response for a specific port, Nmap will set it to that state. This indicates that a firewall or packet filter may protect the port.|
|closedfiltered	|This state only occurs in the IP ID idle scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.|

```sh
sudo nmap 10.129.2.28 --top-ports=10 

sudo nmap 10.129.2.28 -Pn -n --disable-arp-ping --packet-trace -p 445 --reason  -sV
```
### Send Output to a file:
```sh
nmap -oN output.txt # normal
nmap -oX output.xml # xml
nmap -oG output.grep # grepable
nmap -oA output # all formats at once
```
### Nmap XML Output to HTML Output
```sh
xsltproc target.xml -o target.html
```



### Nmap Scripting Engine
```sh
auth	  #Determination of authentication credentials.
broadcast #Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans.
brute	  #Executes scripts that try to log in to the respective service by brute-forcing with credentials.
default	  #Default scripts executed by using the -sC option.
discovery #Evaluation of accessible services.
dos       #These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services.
exploit	  #This category of scripts tries to exploit known vulnerabilities for the scanned port.
external  #Scripts that use external services for further processing.
fuzzer	  #This uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time.
intrusive #Intrusive scripts that could negatively affect the target system.
malware   #Checks if some malware infects the target system.
safe	  #Defensive scripts that do not perform intrusive and destructive access.
version	  #Extension for service detection.
vuln	  #Identification of specific vulnerabilities.
```

### Examples
```sh
sudo nmap 10.129.183.156 -p 20,80,110,139,143,445  -sV --script vuln --min-rate=100000

# Detect OS but appear as 5 random ips
sudo nmap 10.129.21.202 -sV -D RND:5 -p- -vv --stats-every=20s -oN special -vv 

# to not get detected so easy
sudo nmap -O 10.129.21.202 -D RND:10 -T2 -vv --stats-every=20s -oN special -sA 

# with aggressive mode
sudo nmap -O 10.129.21.202 -A -D RND:10 -T2 -vv --stats-every=20s -oN special -sA --top-ports=10 


sudo nmap -O 10.129.2.48 -sV -D RND:10 -T2 -vvv --stats-every=20s -oN special2 -p 53 
```

### sudo nmap Performance
```sh
sudo nmap 10.129.2.0/24 -F #Scans top 100 ports.
sudo nmap 10.129.2.0/24 -F --initial-rtt-timeout 50ms --max-rtt-timeout 100ms
```

### Default Scan - Found Open Ports
```sh 
cat tnet.default | grep "/tcp" | wc -l
```

### Insane Scan - Found Open Ports
```sh 
cat tnet.T5 | grep "/tcp" | wc -l
```

### SYN-Scan 
Nmap's TCP ACK scan (-sA) method is much harder to filter for firewalls and IDS/IPS systems than regular SYN (-sS) or Connect scans (sT) because they only send a TCP packet with only the ACK flag. When a port is closed or open, the host must respond with an RST flag. Unlike outgoing connections, all connection attempts (with the SYN flag) from external networks are usually blocked by firewalls. However, the packets with the ACK flag are often passed by the firewall because the firewall cannot determine whether the connection was first established from the external network or the internal network.
```sh
sudo nmap 10.129.2.28 -p 21,22,25 -sS -Pn -n --disable-arp-ping --packet-trace
```

### ACK-Scan
```sh
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```

## IDS/IPS

Like the firewall, the intrusion detection system (IDS) and intrusion prevention system (IPS) are also software-based components. IDS scans the network for potential attacks, analyzes them, and reports any detected attacks. IPS complements IDS by taking specific defensive measures if a potential attack should have been detected. The analysis of such attacks is based on pattern matching and signatures. If specific patterns are detected, such as a service detection scan, IPS may prevent the pending connection attempts.