## Domain Information

#### SSL Certificates
Check the SSL certificate of the domain.
Some information can be seen.

#### crt.sh
- https://crt.sh/
On this page we can find Certificate Transparency logs.
- https://en.wikipedia.org/wiki/Certificate_Transparency
```sh
#get json of it
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . 

#filtered by the unique subdomains.
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u

# we can identify the hosts directly accessible from the Internet and not hosted by third-party providers
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```

#### Shodan
We can generate a list of IP addresses and run them through Shodan.
```sh
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done
for i in $(cat ip-addresses.txt);do shodan host $i;done
```

#### DNS Records
```sh
dig any inlanefreight.com
```
#### Source code of the page html
Search  for intresting paths, ways and technology behind

### Cloud Resources
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