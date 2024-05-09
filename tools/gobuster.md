# gobuster 
can scan possible paths in websites
Scan an IP Address or DNS Names based on the wordlist

- Can be used to find hidden directories, paths and files
- Can specify a wordlist
- can specify extensions
- can specify threds

### Parameter
```sh
sudo gobuster dir -w /usr/share/wordlists/dirb/common.txt -u 10.129.245.110
-h #help
dir #specify we are using the directory busting mode of the tool 
--url #Specify the web address of the target machine that runs the HTTP server.
-w #specify a wordlist, a collection of common directory names that are typically used for sites 
-u # specify the target's IP address
-x # specify the file extension to search for
-x php.html #example search for files with the extension .php or .html finds more than without it
-r #recursive, search for files in subdirectories and follow redirects
-o: Output file
vhost #find also virtual hosts (subdomains)
```

## Installation
```sh
sudo apt install golang-go
go install github.com/OJ/gobuster/v3@lates
```

## GoBuster - DNS with patterns.txt
#### create patterns.txt
```sh
#patterns .txt content examole 
lert-api-shv-{GOBUSTER}-sin6
atlas-pp-shv-{GOBUSTER}-sin6
```
#### Gobuster - DNS
```sh
export TARGET="facebook.com"
export NS="d.ns.facebook.com"
export WORDLIST="numbers.txt"
gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt" 
```


### Examples
```sh
sudo gobuster dir -w /usr/share/wordlists/dirb/common.txt -u 10.129.245.110
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u 10.129.245.110
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u 10.129.245.110 -x php.html
sudo gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://devvortex.htb/
sudo gobuster dir -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://ignition.htb/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://10.129.253.171:5000/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://devvortex.htb/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://dev.devvortex.htb/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://dev.devvortex.htb/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://dev.devvortex.htb -x php,html,txt,json -r
```

### Wordlists
```sh
/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
/usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
/usr/share/wordlists/dirbuster/directory-list-2.3-big.txt
/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
