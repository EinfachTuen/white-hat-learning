## nmap tool to scan ports

**nmap**

**-sV** switch stands for version detection

**-p-** Omit beginning and end numbers to scan the whole range

**--min-rate=1000** : This is used to specify the minimum number of packets that Nmap should send per second; it speeds up the scan as the number goes higher

**-sC** run with default Scripts (more Infos)

Find informations about ports:
https://www.speedguide.net/port.php?port=3389


## Usual scripts:
```sh
nmap -p- -sV -sC --min-rate=100000 10.129.103.187
```

## Special scripts:

scan without details and than scan with:
```sh
ports=$(nmap -p- --min-rate=1000 -T4 10.129.230.220 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//) nmap -p$ports -sV -sC 10.129.230.220
```
