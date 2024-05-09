## Metasploit
MetaSploit is a framework that is used to exploit vulnerabilities in systems
- written for Pentesters
- written in ruby
- all in one tool
- can be used for scanning, cracking, exploiting, post exploitation
- 
### Usages
```sh
msfdb run #start the metasploit database, keeps track on what found
db_nmap <target-ip> -A #scan a target, Aggressive
hosts #show all hosts in the database, (in this case from nmap)
search <searchterm> #search for a module
info <moduleNo> #get information about a module
use <moduleNo> #use a module
show target #show the target
run #run the module
run -j #would be run the module in the background
exploit #run the module 
sysinfo #get system information
exit #exit the module
ps #show all processes
migrate <pid> #migrate to another process

```

