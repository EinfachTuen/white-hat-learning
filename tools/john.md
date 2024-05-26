## John the Ripper
- https://github.com/openwall/john
- there is a gui based version called Johnny
- not in kali but in parrot
### Cracking a password hash10.10
-w : wordlist to use for cracking the hash

```bash
echo "Administrator::RESPONDER:38349c0ce7942c6d:81425C2D93391D50BA79AF22D25B52BA:010100000000000080D0F79E1F86DA01135337A591EBA2CB0000000002000800310039005000300001001E00570049004E002D0045004400480051004100330042004E004F005700480004003400570049004E002D0045004400480051004100330042004E004F00570048002E0031003900500030002E004C004F00430041004C000300140031003900500030002E004C004F00430041004C000500140031003900500030002E004C004F00430041004C000700080080D0F79E1F86DA0106000400020000000800300030000000000000000100000000200000DC56273D643D897DACDA988F596BA1837445E863ED13AC38A40CF6DE359C4EBA0A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310035002E00370031000000000000000000
" > hash.txt
```

```bash
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

### John the Ripper
```bash
john hash.txt # This will try to crack the hash
john -w=/usr/share/wordlists/rockyou.txt hash.txt # This will try to crack the hash with the rockyou wordlist
john --single hash.txt # This will try to crack the hash with the single mode
john--show hash.txt # This will show the cracked hash, if you open same file again
```

## Cracking Modes

### Single Crack Mode
- brute force attack
- using a single password list

Example
```shell
john --format=<hash_type> <hash or hash_file>

john --format=sha256 hashes_to_crack.txt
# john is the command to run the John the Ripper program
# --format=sha256 specifies that the hash format is SHA-256
# hashes.txt is the file name containing the hashes to be cracked
```

## Wordlist Mode
Wordlist Mode uses multiple wordlists to crack passwords by trying each word until it finds a match. It's a dictionary attack, effective for multiple password hashes, and more thorough than Single Crack Mode. Basic command syntax:
```shell
john --wordlist=<wordlist_file> --rules <hash_file>
```
First, we specify the wordlist file or files to use for cracking the password hashes

## Incremental Mode
Incremental Mode is an advanced John mode that cracks passwords by trying all possible character combinations from a set, making it highly effective but time-consuming. It generates guesses on the fly, unlike Wordlist Mode, which uses a predefined list. This mode is faster than brute force, starting from the shortest combinations, and is useful for cracking weak passwords.
```shell
john --incremental <hash_file>
```
This command reads hashes from a file and generates all possible character combinations, starting with one character and incrementing. It's resource-intensive and time-consuming, depending on password complexity, machine configuration, and character set size. The default set is a-zA-Z0-9; use a custom set for special characters.

## Cracking Files
- john can also be used to crack password protected files
- there for we need additional tools like pdf 2 john

Example:
```shell
<tool> <file_to_crack> > file.hash
pdf2john server_doc.pdf > server_doc.hash
john server_doc.hash
                # OR
john --wordlist=<wordlist.txt> server_doc.hash 
```
### Tool List: 
| Tool                    | Description                              |
|-------------------------|------------------------------------------|
| pdf2john                | Converts PDF documents for John          |
| ssh2john                | Converts SSH private keys for John       |
| mscash2john             | Converts MS Cash hashes for John         |
| keychain2john           | Converts OS X keychain files for John    |
| rar2john                | Converts RAR archives for John           |
| pfx2john                | Converts PKCS#12 files for John          |
| truecrypt_volume2john   | Converts TrueCrypt volumes for John      |
| keepass2john            | Converts KeePass databases for John      |
| vncpcap2john            | Converts VNC PCAP files for John         |
| putty2john              | Converts PuTTY private keys for John     |
| zip2john                | Converts ZIP archives for John           |
| hccap2john              | Converts WPA/WPA2 handshake captures for John |
| office2john             | Converts MS Office documents for John    |
| wpa2john                | Converts WPA/WPA2 handshakes for John    |

- more tools in pwnbox
```shell
locate *2john*
```

## Hash Format
| Hash Format             | Example Command                           | Description                                             |
|-------------------------|-------------------------------------------|---------------------------------------------------------|
| afs                     | john --format=afs hashes_to_crack.txt     | AFS (Andrew File System) password hashes                |
| bfegg                   | john --format=bfegg hashes_to_crack.txt   | bfegg hashes used in Eggdrop IRC bots                   |
| bf                      | john --format=bf hashes_to_crack.txt      | Blowfish-based crypt(3) hashes                          |
| bsdi                    | john --format=bsdi hashes_to_crack.txt    | BSDi crypt(3) hashes                                    |
| crypt(3)                | john --format=crypt hashes_to_crack.txt   | Traditional Unix crypt(3) hashes                        |
| des                     | john --format=des hashes_to_crack.txt     | Traditional DES-based crypt(3) hashes                   |
| dmd5                    | john --format=dmd5 hashes_to_crack.txt    | DMD5 (Dragonfly BSD MD5) password hashes                |
| dominosec               | john --format=dominosec hashes_to_crack.txt| IBM Lotus Domino 6/7 password hashes                    |
| EPiServer SID hashes    | john --format=episerver hashes_to_crack.txt| EPiServer SID (Security Identifier) password hashes     |
| hdaa                    | john --format=hdaa hashes_to_crack.txt    | hdaa password hashes used in Openwall GNU/Linux         |
| hmac-md5                | john --format=hmac-md5 hashes_to_crack.txt| hmac-md5 password hashes                                |
| hmailserver             | john --format=hmailserver hashes_to_crack.txt| hmailserver password hashes                             |
| ipb2                    | john --format=ipb2 hashes_to_crack.txt    | Invision Power Board 2 password hashes                  |
| krb4                    | john --format=krb4 hashes_to_crack.txt    | Kerberos 4 password hashes                              |
| krb5                    | john --format=krb5 hashes_to_crack.txt    | Kerberos 5 password hashes                              |
| LM                      | john --format=LM hashes_to_crack.txt      | LM (Lan Manager) password hashes                        |
| lotus5                  | john --format=lotus5 hashes_to_crack.txt  | Lotus Notes/Domino 5 password hashes                    |
| mscash                  | john --format=mscash hashes_to_crack.txt  | MS Cache password hashes                                |
| mscash2                 | john --format=mscash2 hashes_to_crack.txt | MS Cache v2 password hashes                             |
| mschapv2                | john --format=mschapv2 hashes_to_crack.txt| MS CHAP v2 password hashes                              |
| mskrb5                  | john --format=mskrb5 hashes_to_crack.txt  | MS Kerberos 5 password hashes                           |
| mssql05                 | john --format=mssql05 hashes_to_crack.txt | MS SQL 2005 password hashes                             |
| mssql                   | john --format=mssql hashes_to_crack.txt   | MS SQL password hashes                                  |
| mysql-fast              | john --format=mysql-fast hashes_to_crack.txt| MySQL fast password hashes                             |
| mysql                   | john --format=mysql hashes_to_crack.txt   | MySQL password hashes                                   |
| mysql-sha1              | john --format=mysql-sha1 hashes_to_crack.txt| MySQL SHA1 password hashes                             |
| NETLM                   | john --format=netlm hashes_to_crack.txt   | NETLM (NT LAN Manager) password hashes                  |
| NETLMv2                 | john --format=netlmv2 hashes_to_crack.txt | NETLMv2 (NT LAN Manager version 2) password hashes      |
| NETNTLM                 | john --format=netntlm hashes_to_crack.txt | NETNTLM (NT LAN Manager) password hashes                |
| NETNTLMv2               | john --format=netntlmv2 hashes_to_crack.txt| NETNTLMv2 (NT LAN Manager version 2) password hashes    |
| NEThalfLM               | john --format=nethalflm hashes_to_crack.txt| NEThalfLM (NT LAN Manager) password hashes              |
| md5ns                   | john --format=md5ns hashes_to_crack.txt   | md5ns (MD5 namespace) password hashes                   |
| nsldap                  | john --format=nsldap hashes_to_crack.txt  | nsldap (OpenLDAP SHA) password hashes                   |
| ssha                    | john --format=ssha hashes_to_crack.txt    | ssha (Salted SHA) password hashes                       |
| NT                      | john --format=nt hashes_to_crack.txt      | NT (Windows NT) password hashes                         |
| openssha                | john --format=openssha hashes_to_crack.txt| OPENSSH private key password hashes                     |
| oracle11                | john --format=oracle11 hashes_to_crack.txt| Oracle 11 password hashes                               |
| oracle                  | john --format=oracle hashes_to_crack.txt  | Oracle password hashes                                  |
| pdf                     | john --format=pdf hashes_to_crack.txt     | PDF (Portable Document Format) password hashes          |
| phpass-md5              | john --format=phpass-md5 hashes_to_crack.txt| PHPass-MD5 (Portable PHP password hashing framework) password hashes|
| phps                    | john --format=phps hashes_to_crack.txt    | PHPS password hashes                                    |
| pix-md5                 | john --format=pix-md5 hashes_to_crack.txt | Cisco PIX MD5 password hashes                           |
| po                      | john --format=po hashes_to_crack.txt      | Po (Sybase SQL Anywhere) password hashes                |
| rar                     | john --format=rar hashes_to_crack.txt     | RAR (WinRAR) password hashes                            |
| raw-md4                 | john --format=raw-md4 hashes_to_crack.txt | Raw MD4 password hashes                                 |
| raw-md5                 | john --format=raw-md5 hashes_to_crack.txt | Raw MD5 password hashes                                 |
| raw-md5-unicode         | john --format=raw-md5-unicode hashes_to_crack.txt| Raw MD5 Unicode password hashes                    |
| raw-sha1                | john --format=raw-sha1 hashes_to_crack.txt| Raw SHA1 password hashes                                |
| raw-sha224              | john --format=raw-sha224 hashes_to_crack.txt| Raw SHA224 password hashes                            |
| raw-sha256              | john --format=raw-sha256 hashes_to_crack.txt| Raw SHA256 password hashes                            |
| raw-sha384              | john --format=raw-sha384 hashes_to_crack.txt| Raw SHA384 password hashes                            |
| raw-sha512              | john --format=raw-sha512 hashes_to_crack.txt| Raw SHA512 password hashes                            |
| salted-sha              | john --format=salted-sha hashes_to_crack.txt| Salted SHA password hashes                            |
| sapb                    | john --format=sapb hashes_to_crack.txt    | SAP CODVN B (BCODE) password hashes                     |
| sapg                    | john --format=sapg hashes_to_crack.txt    | SAP CODVN G (PASSCODE) password hashes                  |
| sha1-gen                | john --format=sha1-gen hashes_to_crack.txt| Generic SHA1 password hashes                            |
| skey                    | john --format=skey hashes_to_crack.txt    | S/Key (One-time password) hashes                        |
| ssh                     | john --format=ssh hashes_to_crack.txt     | SSH (Secure Shell) password hashes                      |
| sybasease               | john --format=sybasease hashes_to_crack.txt| Sybase ASE password hashes                              |
| xsha                    | john --format=xsha hashes_to_crack.txt    | xsha (Extended SHA) password hashes                     |
| zip                     | john --format=zip hashes_to_crack.txt     | ZIP (WinZip) password hashes                            |

