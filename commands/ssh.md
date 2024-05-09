# SSH
Secure Shell (SSH)
- Replaced telnet
- Asymmetric encryption (key pairs)
- port 22 (but often changed)
- Stable
- Tab completion
- History
- sftp File Transfer

### OpenSSH Authentication Methods
OpenSSH has six different authentication methods:
- Password authentication
- Public-key authentication
- Host-based authentication
- Keyboard authentication
- Challenge-response authentication
- GSSAPI authentication

## Configuration
### Default Configuration
The sshd_config file, responsible for the OpenSSH server, has only a few of the settings configured by default.
```sh
cat /etc/ssh/sshd_config  | grep -v "#" | sed -r '/^\s*$/d'
  
  Include /etc/ssh/sshd_config.d/*.conf
  ChallengeResponseAuthentication no
  UsePAM yes
  X11Forwarding yes
  PrintMotd no
  AcceptEnv LANG LC_*
  Subsystem       sftp    /usr/lib/openssh/sftp-server
```
### Dangerous Settings:
| Setting                  | Description                                        |
|--------------------------|----------------------------------------------------|
| PasswordAuthentication   | Allows password-based authentication.              |
| PermitEmptyPasswords     | Allows the use of empty passwords.                 |
| PermitRootLogin          | Allows to log in as the root user.                 |
| Protocol                 | Uses an outdated version of encryption.            |
| X11Forwarding            | Allows X11 forwarding for GUI applications.        |
| AllowTcpForwarding       | Allows forwarding of TCP ports.                    |
| PermitTunnel             | Allows tunneling.                                  |
| DebianBanner             | Displays a specific banner when logging in.        |

## Parameter
```sh
ssh test@123.254.1.1 -t sh
-t # shell type (f.e sh, bash)
-D # dynamic port forwarding
-L # local port forwarding
-R # remote port forwarding
- # login with keyfile
```

## Good to know
can directly execute commands
```sh
ssh test@123.254.1.1 cat /etc/passwd #execute command cat
```
### Exapmple with key

```shell
ssh -i id_rsa ceil@10.129.42.195

```
#### SSH Key Generation:
```sh
ssh-keygen
```

## Port Forwarding:
Port forwarding redirects data from one IP and port to another, often used in attack scenarios.

### Local Port Forwarding:
Local Port Forwarding is used to forward a port from the client machine to the server machine.
```sh
ssh -L <local-port>:<remote-ip>:<remote-port> <user>@<remote-ip>
```
### Remote Port Forwarding:
Remote Port Forwarding is used to forward a port from the server machine to the client machine.
```sh
ssh -R <remote-port>:localhost:<local-port> <user>@<remote-ip>
```
### Dynamic Port Forwarding:
Dynamic Port Forwarding via SSH creates a secure connection for any TCP/UDP port forwarding.
```sh

ssh -D <local-port> <user>@<remote-ip>
```

### Examples:

```sh
ssh -L 1234:localhost:22 user@remote.example.com
```
#### Example both same:
1. Local Port Forwarding
```sh
#Forwards http traffic from port 1234 on the local machine to port 80 on target machine
# so localhost:1234 -> is 192.168.1.49:80
ssh -L 1234:10.10.52.23:80 user@192.168.1.49
```
2. Dynamic Port Forwarding
```sh
# This does the same as the above command, but it forwards to all ports on the target machine
# Dynamic Port Forwarding
sudo ssh -N -D 127.0.0.1 root@192.168.1.49
# tool proxy chain
proxychains curl -v http://10.10.52.23 #use proxychains to use the ssh tunnel 
```


#### From htb guide:
```sh
#In the scenario we are currently facing, we want to forward traffic from any given local port, for instance
#1234 , to the port on which PostgreSQL is listening, namely 5432 , on the remote server. We therefore
#specify port 1234 to the left of localhost , and 5432 to the right, indicating the target port.
ssh -L 1234:localhost:5432 christine@10.129.228.195
```
## Footprinting
### SSH Audit
```sh
git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit
./ssh-audit.py 10.129.14.132
```
### Change Authentication Method
```sh
ssh -v cry0l1t3@10.129.14.132
ssh -v cry0l1t3@10.129.14.132 -o PreferredAuthentications=password
```

### SSH Logins:
- username:password
- Key files
  - typically in following locations:
  - /home/user/.ssh/id_rsa
  - /home/user/.ssh/id_rsa.pub
  - /home/user/.ssh/authorized_keys
  - keyfile can also have a password
- or Combination of both login methods so username and keyfile

### SSH Login Brute Force:
In CTFs usually no lockout or ban by blueteam / firewall for try to bruteforce ssh
```sh
hydra -l <username> -P /usr/share/wordlists/rockyou.txt <target-ip> ssh
```
### SSH Login by adding key to authorized keys:

```shell
#1. create SSH key on local machine
ssh-keygen  
#2. put ssh key to authorized keys at target file system
cat ~/.ssh/id_rsa.pub >> ~/mnt/nfs/root/.ssh/authorized_keys #>> appends to file
#3. ssh into it machine
ssh root@192.253.1.35 
```