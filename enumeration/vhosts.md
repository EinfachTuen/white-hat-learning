# VHOST

## Curl
### Curl normal
```shell
curl -s http://192.168.10.10

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
### Curl with Host header
```shell
curl -s http://192.168.10.10 -H "Host: randomtarget.com"

<html>
    <head>
        <title>Welcome to randomtarget.com!</title>
    </head>
    <body>
        <h1>Success! The randomtarget.com server block is working!</h1>
    </body>
</html>
```
Now we can automate this by using a dictionary file of possible vhost names (such as /opt/useful/SecLists/Discovery/DNS/namelist.txt on the Pwnbox) and examining the Content-Length header to look for any differences.
### Vhost Fuzzing
```shell
echo "app" > vhosts
echo "blog" >> vhosts
echo "dev-admin" >> vhosts
echo "forum" >> vhosts
echo "help" >> vhosts
echo "m" >> vhosts
echo "my" >> vhosts
echo "shop" >> vhosts
echo "some" >> vhosts
echo "store" >> vhosts
echo "support" >> vhosts
echo "www" >> vhosts

cat ./vhosts | while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://192.168.10.10 -H "HOST: ${vhost}.randomtarget.com" | grep "Content-Length: ";done
```
## for Fuff see fuff.md
