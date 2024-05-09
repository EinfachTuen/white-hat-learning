# Domain Information passive

### SSL Certificates
Check the SSL certificate of the domain.
Some information can be seen.

### crt.sh
- https://crt.sh/
On this page we can find Certificate Transparency logs.
- https://en.wikipedia.org/wiki/Certificate_Transparency
```sh
#get json of it
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . 

#another way
export TARGET="facebook.com"
curl -s "https://crt.sh/?q=${TARGET}&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "${TARGET}_crt.sh.txt"
head -n20 facebook.com_crt.sh.txt

#filtered by the unique subdomains.
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u

# we can identify the hosts directly accessible from the Internet and not hosted by third-party providers
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```
### censys.io
https://censys.io

### Virus Total
- https://www.virustotal.com/gui/home/url

VirusTotal maintains its DNS replication service, which is developed by preserving DNS resolutions made when users visit URLs given by them.

### Netcraft
Netcraft can offer us information about the servers without even interacting with them
https://sitereport.netcraft.com

### Wayback Machine
to find old versions that may have interesting comments
https://web.archive.org/

#### waybackurls to inspect URLs saved by Wayback Machine
```shell 
go install github.com/tomnomnom/waybackurls@latest

#To get a list of crawled URLs from a domain with the date it was obtained, we can add the -dates switch to our command as follows:
waybackurls -dates https://facebook.com > waybackurls.txt
cat waybackurls.txt
#2018-05-20T09:46:07Z http://www.facebook.com./
#2018-05-20T10:07:12Z https://www.facebook.com/
#2018-05-20T10:18:51Z http://www.facebook.com/#!/pages/Welcome-Baby/143392015698061?ref=tsrobots.txt
#2018-05-20T10:19:19Z http://www.facebook.com/
#2018-05-20T16:00:13Z http://facebook.com
#2018-05-21T22:12:55Z https://www.facebook.com
#2018-05-22T15:14:09Z http://www.facebook.com
#2018-05-22T17:34:48Z http://www.facebook.com/#!/Syerah?v=info&ref=profile/robots.txt
#2018-05-23T11:03:47Z http://www.facebook.com/#!/Bin595
```

### Shodan
We can generate a list of IP addresses and run them through Shodan.
```sh
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done
for i in $(cat ip-addresses.txt);do shodan host $i;done
```


### via OpenSSL
```sh
export TARGET="facebook.com"
export PORT="443"
openssl s_client -ign_eof 2>/dev/null <<<$'HEAD / HTTP/1.0\r\n\r' -connect "${TARGET}:${PORT}" | openssl x509 -noout -text -in - | grep 'DNS' | sed -e 's|DNS:|\n|g' -e 's|^\*.*||g' | tr -d ',' | sort -u
```
### DNS Records
```sh
dig any inlanefreight.com
```
### Source code of the page html
Search  for intresting paths, ways and technology behind

## The Harvester
TheHarvester is a simple-to-use yet powerful and effective tool for early-stage penetration testing and red team engagements. We can use it to gather information to help identify a company's attack surface. The tool collects emails, names, subdomains, IP addresses, and URLs from various public data sources for passive information gathering.
- https://github.com/laramies/theHarvester
### Harvester all sources Script
```shell
#get the script from github

cat sources.txt
# create a file with this content
baidu
bufferoverun
crtsh
hackertarget
otx
projectdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye
```
#### Execute it
```shell
export TARGET="facebook.com"
cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done
```
#### Find and sort and merge output
```shell
cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f 1 | sort -u > "${TARGET}_theHarvester.txt"
cat facebook.com_*.txt | sort -u > facebook.com_subdomains_passive.txt
cat facebook.com_subdomains_passive.txt | wc -l
```


## Cloud Resources
- cloud storage can be added to dns lis
```sh
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```
-we can search on google for more informations about url and provider

#### Domain.glass Results
- https://domain.glass/

#### GrayhatWarfare
- https://buckets.grayhatwarfare.com/
shows also leaked keys etc.

#### Staff
- LinkedIn, Employees profiles, Github, Links, Best practices
- Xing
- Facebook 
- Job posts, Technology, Phising, etc.
