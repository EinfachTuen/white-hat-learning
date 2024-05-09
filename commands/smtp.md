## SMTP

Simple Mail Transfer Protocol (SMTP)
- used to send, receive and relay emails
- uses port 25 or newer other f.e. 587 or 465 SSL
- Attacks: user enumeration and relay to send spam or phising mails


### SMTP Configuration
```sh
cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"

smtpd_banner = ESMTP Server 
biff = no
append_dot_mydomain = no
readme_directory = no
compatibility_level = 2
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache
myhostname = mail1.inlanefreight.htb
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
smtp_generic_maps = hash:/etc/postfix/generic
mydestination = $myhostname, localhost 
masquerade_domains = $myhostname
mynetworks = 127.0.0.0/8 10.129.0.0/16
mailbox_size_limit = 0
recipient_delimiter = +
smtp_bind_address = 0.0.0.0
inet_protocols = ipv4
smtpd_helo_restrictions = reject_invalid_hostname
home_mailbox = /home/postfix
```

| Command    | Description                                                                                   |
|------------|-----------------------------------------------------------------------------------------------|
| AUTH PLAIN | AUTH is a service extension used to authenticate the client.                                  |
| HELO       | The client logs in with its computer name and thus starts the session.                        |
| MAIL FROM  | The client names the email sender.                                                           |
| RCPT TO    | The client names the email recipient.                                                        |
| DATA       | The client initiates the transmission of the email.                                           |
| RSET       | The client aborts the initiated transmission but keeps the connection between client and server. |
| VRFY       | The client checks if a mailbox is available for message transfer.                            |
| EXPN       | The client also checks if a mailbox is available for messaging with this command.            |
| NOOP       | The client requests a response from the server to prevent disconnection due to time-out.     |
| QUIT       | The client terminates the session.                                                           |

### SMTP Enumeration

#### Nmap
- https://nmap.org/nsedoc/scripts/smtp-open-relay.html
```sh
sudo nmap --script smtp* -p 25 <target-ip>    
sudo nmap 10.129.159.200 -sC -sV -p25

#nmap open relay
sudo nmap 10.129.159.200 -p25 --script smtp-open-relay -v 
```

### Telnet
- we can use the telnet tool to initialize a TCP connection with the SMTP server

#### Telnet - HELO/EHLO
```sh
telnet 10.129.14.128 25
    
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 


HELO mail1.inlanefreight.htb

250 mail1.inlanefreight.htb


EHLO mail1

250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING
```
#### Telnet - VRFY
```sh
telnet 10.129.159.200 25
    
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 
VRFY root
252 2.0.0 root
VRFY cry0l1t3
252 2.0.0 cry0l1t3
VRFY testuser
252 2.0.0 testuser
VRFY aaaaaaaaaaaaaaaaaaaaaaaaaaaa
252 2.0.0 aaaaaaaaaaaaaaaaaaaaaaaaaaaa
```
Sometimes we may have to work through a web proxy. We can also make this web proxy connect to the SMTP server. The command that we would send would then look something like this: 
```
CONNECT 10.129.14.128:25 HTTP/1.0
```

#### Send an Email
```sh
[!bash!]$ telnet 10.129.14.128 25

Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server


EHLO inlanefreight.htb

250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING


MAIL FROM: <cry0l1t3@inlanefreight.htb>

250 2.1.0 Ok


RCPT TO: <mrb3n@inlanefreight.htb> NOTIFY=success,failure

250 2.1.5 Ok


DATA
```
### NCat
Ncat "Manual Enumeration" can give more informations
```sh
nc -C 10.129.159.200 25

# The -C flag in the nc command sends CRLF as line-ending. 
# This is particularly useful when interacting with a server that expects Windows-style line endings.  
# the context of your code, 
# nc -C <target-ip> 25 is used to establish a connection to the SMTP server at the target IP address on port 25, 
# sending CRLF as line-ending.
```

### smtp-user-enum
Also enumerates more
```sh
smtp-user-enum -M VRFY -U users.txt -t  10.129.159.200 -w 20
```


### Exploring SMTP

#### njstar metasploit exloit

This is full Metasploit Exploit which creates a shell if attackable
```sh
msfconsole
search njstar # njstar Communicator 3.0 SMTP Buffer Overflow
use 0 #use the found exploit
show options #(optional) show options just to get infos
set RHOSTS <target-ip>
```