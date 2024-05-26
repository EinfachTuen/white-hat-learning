# Hashcat

```bash
hashid hash.txt # This will tell you what type of hash it is
```

## Password Mutations
| Description                              | Password          |
|------------------------------------------|-------------------|
| First letter is uppercase.               | Password          |
| Adding numbers.                          | Password123       |
| Adding year.                             | Password2022      |
| Adding month.                            | Password02        |
| Last character is an exclamation mark.   | Password2022!     |
| Adding special characters.               | P@ssw0rd2022!     |

### Rule File
| Function | Description                                       |
|----------|---------------------------------------------------|
| :        | Do nothing.                                       |
| l        | Lowercase all letters.                            |
| u        | Uppercase all letters.                            |
| c        | Capitalize the first letter and lowercase others. |
| sXY      | Replace all instances of X with Y.                |
| $!       | Add the exclamation character at the end.         |

Example for rule file content
```shell 
cat custom.rule
#:
#c
#so0
#c so0
#sa@
#c sa@
#c sa@ so0
#$!
#$! c
#$! so0
#$! sa@
#$! c so0
#$! c sa@
#$! so0 sa@
#$! c so0 sa@
```

## prebuilt Rule Lists:
```shell
ls /usr/share/hashcat/rules/

best64.rule                  specific.rule
combinator.rule              T0XlC-insert_00-99_1950-2050_toprules_0_F.rule
rockyou-30000.rule           ...
```


### Example Password mutations:
```bash
cat password.list
# password

hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
cat mut_password.list
#password
#Password
#passw0rd
#Passw0rd
#p@ssword
#P@ssword
#P@ssw0rd
#password!
#Password!
#passw0rd!
#p@ssword!
#Passw0rd!
#P@ssword!
#p@ssw0rd!
#P@ssw0rd!
```

### Generating Wordlists Using CeWL
- scans word from website and than create wordlist
```bash
cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist
wc -l inlane.wordlist
```