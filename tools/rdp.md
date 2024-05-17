# RDP
- Remote Desktop Protocol (RDP) 
- https://learn.microsoft.com/en-us/troubleshoot/windows-server/remote/understanding-remote-desktop-protocol
- TLS /SSL since windows vista
- many Windows systems do not insist on this but still accept inadequate encryption via RDP Security.
- https://en.wikipedia.org/wiki/Remote_Desktop_Services#Network_Level_Authentication


## Footprinting

### Nmap
```sh
sudo nmap -sV -sC 10.129.201.248 -p3389 --script rdp* 

sudo nmap -sV -sC 10.129.201.248 -p3389 --packet-trace --disable-arp-ping -n
#In addition, we can use --packet-trace to track the individual packages and inspect their contents manually. We can see that the RDP cookies (mstshash=nmap) used by Nmap 
# to interact with the RDP server can be identified by threat hunters and various security 
# services such as Endpoint Detection and Response (EDR), and can lock us out as penetration testers on hardened networks.

nmap -sV -sC 10.129.201.248 -p3389 --packet-trace --disable-arp-ping -n #nmap RDP scan with packet trace and no arp ping
```

### RDP Sec Scan Script
```sh
sudo cpan #install cpan
git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check #clone the repo
./rdp-sec-check.pl 10.129.201.248 #scan the target

```

### Connect
Authentication and connection to such RDP servers can be made in several ways. For example, we can connect to RDP servers on Linux using xfreerdp, rdesktop, or Remmina and interact with the GUI of the server accordingly.

#### Initiate an RDP Session
```sh
xfreerdp /u:htb-student /p:"HTB_@cademy_stdnt!" /v:10.129.201.55
```
After successful authentication, a new window will appear with access to the server's desktop to which we have connected.