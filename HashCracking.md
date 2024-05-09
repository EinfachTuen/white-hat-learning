## Hash Cracking 

### Online Ressources
- Crackstation (https://crackstation.net/)
- md5hashing (https://md5hashing.net/hash)
- Cyberchef (https://gchq.github.io/CyberChef/)

```bash
hashid hash.txt # This will tell you what type of hash it is
hashid '$P' # This will tell you what type of hash it is
```

### John the Ripper
```bash
john hash.txt # This will try to crack the hash
john -w=/usr/share/wordlists/rockyou.txt hash.txt # This will try to crack the hash with the rockyou wordlist
john --single hash.txt # This will try to crack the hash with the single mode
john--show hash.txt # This will show the cracked hash, if you open same file again
```

### Hashcat
- is much faster
- must specify hash type id
- uses gpu

```bash
hashcat -m 0 forHash.txt /usr/share/wordlists/rockyou.txt # This will try to crack the hash with the rockyou wordlist
# -m 0 is for MD5
```

##