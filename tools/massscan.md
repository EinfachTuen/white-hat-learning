## Massscan
(this guide will be improved)
### Masscan: Good to knows
```
- need to specify ports
- no dns resolution only ip addresses
- Syn scan only, (must be super user)
- doesnt ping hosts first
- scans completly randomized
- send using raw libcap (data link layer)

Exkurs: The statement "send using raw libcap (data link layer)" 
refers to how the Masscan tool operates when performing network scanning.  
Masscan uses the libcap library, which is a portable library for network traffic capture. 
This library provides a direct interface with the network card, 
allowing Masscan to send packets directly to the Data Link Layer (Layer 2) of the OSI model. 
This is often referred to as "raw" packet sending.
```

### Example uses
```sh 
iptables -A INPUT -p tcp --dport 82000 -j DROP #need to drop the port to use it as source port
masscan 10.0.0.0/8 -p80,8000-8100 --rate=1000 --source-port 82000 --banners

masscan 10.0.0.0/8 -p80,8000-8100 --rate=1000 --source-ip 192.168.1.5 --banners
```




