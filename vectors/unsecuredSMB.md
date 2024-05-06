## unsecured SMB

in case of this hack the box the port was hidden / inaktive
```sh
nmap -p- -sV -sC -Pn --min-rate=100000 10.129.206.31
```


```sh
sudo apt install smbclient
```

```sh
smbclient -L 10.129.206.31 -U Administrator

smbclient \\\\10.129.206.31\\ADMIN$ -U Administrator #with folder ADMIN$
smbclient \\\\10.129.206.31\\AC$ -U Administrator #with folder C



```