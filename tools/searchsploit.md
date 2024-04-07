## Searchsploit
Searchsploit is a command line search tool for Exploit Database that also allows you to take a look at the exploit details. It is a part of the Metasploit Framework. Searchsploit is a great tool for finding exploits for a specific service or software. It is also useful for finding out if a specific exploit is available or not.

### Good to Know
- Always read what the exploit does before download and  using it
- 
### Example
```sh
searchsploit apache 2.4.7 # search for an exploit for apache 2.4.7
searchsploit -m php/remote/29316.py # copy the exploit to the current directory
searchsploit -u # update the searchsploit database
searchsploit -p 29316 # show the exploit in the terminal, number is the id of the exploit
```