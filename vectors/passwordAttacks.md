# Password Attacks

# Linux
- Linux User auth details: https://tldp.org/HOWTO/pdf/User-Authentication-HOWTO.pdf
## /etc/shadow 
 Linux-based systems handle everything in the form of a file
- /etc/shadow stores the hashed passwords of users
- The /etc/shadow file has a unique format in which the entries are entered and saved when new users are created.

### Content, Example:
```shell
htb-student:$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:18955:0:99999:7:::
```
| Field              | Description                | Example                           |
|--------------------|----------------------------|-----------------------------------|
| Username           | User's login name          | htb-student                       |
| Encrypted Password | User's password hash       | $y$j9T$3QSBB6CbHEu...SNIP...f8Ms  |
| Day of Last Change | Days since Jan 1, 1970     | 18955                             |
| Min Age            | Minimum password age (days)| 0                                 |
| Max Age            | Maximum password age (days)| 99999                             |
| Warning Period     | Days before password expiry| 7                                 |
| Inactivity Period  | Days after password expiry |                                   |
| Expiration Date    | Account expiration date    |                                   |
| Reserved Field     | Reserved for future use    |                                   |

### Shadow Encrypted Password Format
The encryption of the password in this file is formatted as follows:

| Component | Description     | Example                 |
|-----------|-----------------|-------------------------|
| `<id>`    | Identifier      | y                       |
| `<salt>`  | Salt            | j9T                     |
| `<hashed>`| Hashed password | 3QSBB6CbHEu...SNIP...f8Ms |


### Hashid in shadow Encryption
The type (id) is the cryptographic hash method used to encrypt the password. Many different cryptographic hash methods were used in the past and are still used by some systems today.

| ID      | Cryptographic Hash Algorithm |
|---------|------------------------------|
| $1$     | MD5                          |
| $2a$    | Blowfish                     |
| $5$     | SHA-256                      |
| $6$     | SHA-512                      |
| $sha1$  | SHA1crypt                    |
| $y$     | Yescrypt                     |
| $gy$    | Gost-yescrypt                |
| $7$     | Scrypt                       |

## /etc/passwd
The x in the password field indicates that the encrypted password is in the /etc/shadow file. However, if /etc/shadow has incorrect permissions, it can be manipulated, potentially allowing root login without a password. An empty password field means the user can log in without a password.

Example:
```shell
 cat /etc/passwd
 htb-student:x:1000:1000:,,,:/home/htb-student:/bin/bash 
 ```
| Field                        | Description                               | Example               |
|------------------------------|-------------------------------------------|-----------------------|
| `<username>`                 | User's login name                         | htb-student           |
| `<password>`                 | Placeholder for the password field (usually 'x' indicating shadow password file is used) | x                     |
| `<uid>`                      | User ID                                   | 1000                  |
| `<gid>`                      | Group ID                                  | 1000                  |
| `<comment>`                  | User's full name or comment field         | ,,,,                  |
| `<home directory>`           | User's home directory                     | /home/htb-student     |
| `<cmd executed after logging in>` | Command or shell executed after login  | /bin/bash             |


# Windows:
- https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication

| Authentication Package | Description |
|------------------------|-------------|
| Lsasrv.dll             | LSA Server service enforcing security policies and managing the security package. |
| Msv1_0.dll             | Local machine logon authentication without custom authentication. |
| Samsrv.dll             | Manages local security accounts and policies, supports APIs. |
| Kerberos.dll           | Kerberos-based authentication package loaded by the LSA. |
| Netlogon.dll           | Network-based logon service. |
| Ntdsa.dll              | Creates new records and folders in the Windows registry. |

## SAM Database
is a database file in Windows operating systems that stores users' passwords
- https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc756748(v=ws.10)?redirectedfrom=MSDN
- %SystemRoot%/system32/config/SAM
- the SYSKEY (syskey.exe) when enabled, partially encrypts the hard disk copy of the SAM file so that the password hash values for all local accounts stored in the SAM are encrypted with a key.

## Credential Manager
Credential Manager is a built-in Windows feature that allows users to save credentials for network resources and websites, storing them in each user's encrypted Credential Locker based on user profiles.
- C:\Users\[Username]\AppData\Local\Microsoft\[Vault/Credentials]\

There are various methods to decrypt credentials saved using Credential Manager.

## NTDS
In network environments, Windows systems often join a Windows domain for centralized management. These systems send logon requests to Domain Controllers in the same Active Directory forest. Each Domain Controller hosts the NTDS.dit file, synchronized across all Domain Controllers except Read-Only ones. NTDS.dit stores Active Directory data, including:

- User accounts (username & password hash)
- Group accounts
- Computer accounts
- Group policy objects
