## gobuster can scan possible paths in websites
sudo apt install golang-go
go install github.com/OJ/gobuster/v3@lates

**gobuster**

-h : help

dir : specify we are using the directory busting mode of the tool 

--url : Specify the web address of the target machine that runs the HTTP server.

-w : specify a wordlist, a collection of common directory names that are typically used for sites 

-u : specify the target's IP address

-x : specify the file extension to search for

-x php.html : search for files with the extension .php or .html finds more than without it


Scan an IP Address by routes based on the wordlist
```sh
sudo gobuster dir -w /usr/share/wordlists/dirb/common.txt -u 10.129.245.110


sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u 10.129.245.110

sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u 10.129.245.110 -x php.html


```

http://unika.htb/