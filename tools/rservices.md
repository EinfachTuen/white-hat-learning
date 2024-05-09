# R-Services
 suite of services hosted to enable remote access or issue commands between Unix hosts over TCP/IP. 
 - on standard before ssh
 - transfers unencrypted 
 - ports 512-514

## R-Commands
R-Services are only accessible through a suite of programs known as r-commands: https://en.wikipedia.org/wiki/Berkeley_r-commands

### commands
- rcp (remote copy)
- rexec (remote execution)
- rlogin (remote login)
- rsh (remote shell)
- rstat
- ruptime
- rwho (remote who)
 
| Command | Service Daemon | Port | Transport Protocol | Description                                                                                                     |
|---------|----------------|------|--------------------|-----------------------------------------------------------------------------------------------------------------|
| rcp     | rshd           | 514  | TCP                | Copies files bidirectionally between systems like the cp command, without overwrite warnings.                   |
| rsh     | rshd           | 514  | TCP                | Opens a shell on a remote machine, using trusted entries in /etc/hosts.equiv and .rhosts for validation.        |
| rexec   | rexecd         | 512  | TCP                | Runs shell commands on a remote machine with username and password authentication, affected by trusted entries. |
| rlogin  | rlogind        | 513  | TCP                | Logs into a remote Unix-li


## Footprinting
### Nmap
```shell
sudo nmap -sV -p 512,513,514 10.0.17.2
```


### Access Control & Trusted Relationships
The main issue with r-services, which led to their replacement by SSH, is their weak access control. These protocols rely on trusted information from the remote client for authentication.
- default uses PAM for auth https://debathena.mit.edu/trac/wiki/PAM

#### Thrusted hosts
file is recognized as the global configuration regarding all users on a system
```shell
cat /etc/hosts.equiv

    # <hostname> <local username>
    pwnbox cry0l1t3
```

#### .rhosts File
provides a per-user configuration.
```shell
cat .rhosts
    
    htb-student     10.0.17.5
    +               10.0.17.10
    +               +
```
#### Logging in Using Rlogin
```shell
rlogin 10.0.17.2 -l htb-student
```
#### Listing Authenticated Users Using Rwho
```shell
rwho
```
#### Listing Authenticated Users Using Rusers
```shell
rusers -al 10.0.17.5
```

