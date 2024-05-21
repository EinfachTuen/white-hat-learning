# Infiltrating Unix/Linux

## Questions that will help to find the right vector
- What distribution of Linux is the system running?
- What shell & programming languages exist on the system?
- What function is the system serving for the network environment it is on?
- What application is the system hosting?
- Are there any known vulnerabilities?

## Enumerate the Host
```shell
nmap -sC -sV 10.129.125.242
```
## Discovering a Vulnerability
- search in all sources like metasploit or exploit db for usables exploits of all found protokolls, software and versions accessable on the target system
- order by your experience according to the change of success

## Getting full shell 
- When we drop into the system shell, we notice that no prompt is present
```shell
#find python with
which python
#this can be used to get full shell
python -c 'import pty; pty.spawn("/bin/sh")' 
```