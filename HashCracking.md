## Hash Cracking 

| Encryption Technology                     | Description                                                                                                 |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| UNIX crypt(3)                             | Crypt(3) is a traditional UNIX encryption system with a 56-bit key.                                          |
| Traditional DES-based                     | DES-based encryption uses the Data Encryption Standard algorithm to encrypt data.                            |
| bigcrypt                                  | Bigcrypt is an extension of traditional DES-based encryption. It uses a 128-bit key.                         |
| BSDI extended DES-based                   | BSDI extended DES-based encryption is an extension of the traditional DES-based encryption and uses a 168-bit key. |
| FreeBSD MD5-based (Linux & Cisco)         | FreeBSD MD5-based encryption uses the MD5 algorithm to encrypt data with a 128-bit key.                      |
| OpenBSD Blowfish-based                    | OpenBSD Blowfish-based encryption uses the Blowfish algorithm to encrypt data with a 448-bit key.            |
| Kerberos/AFS                              | Kerberos and AFS are authentication systems that use encryption to ensure secure entity communication.       |
| Windows LM                                | Windows LM encryption uses the Data Encryption Standard algorithm to encrypt data with a 56-bit key.         |
| DES-based tripcodes                       | DES-based tripcodes are used to authenticate users based on the Data Encryption Standard algorithm.          |
| SHA-crypt hashes                          | SHA-crypt hashes are used to encrypt data with a 256-bit key and are available in newer versions of Fedora and Ubuntu. |
| SHA-crypt and SUNMD5 hashes (Solaris)     | SHA-crypt and SUNMD5 hashes use the SHA-crypt and MD5 algorithms to encrypt data with a 256-bit key and are available in Solaris. |
... and much more

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

## Type of Attacks 
### Dictionary Attacks
Dictionary attacks use a pre-generated list of words and phrases (a dictionary) to crack passwords by comparing these strings to hashed passwords. The dictionary can come from various sources, such as public dictionaries or leaked passwords. If a match is found, the password is cracked. To mitigate these attacks, use complex and unique passwords, change them regularly, and enable two-factor authentication.

### Brute Force Attacks
Brute force attacks try every possible character combination to crack passwords. This method is slow and more effective against shorter passwords. To increase security, use passwords that are at least 8 characters long and include letters, numbers, and symbols.

### Rainbow Table Attacks
Rainbow table attacks use pre-computed tables of hashes and their plaintext equivalents, making them faster than brute-force attacks. However, they are limited by the size of the rainbow table and only work for hashes included in the table. Larger tables increase the likelihood of success.
