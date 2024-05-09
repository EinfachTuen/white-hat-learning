## DNS
- Domain Name System (DNS) 

| Server Type                | Description                                                                                                                                                                         |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DNS Root Server            | Root servers manage top-level domains (TLDs) and are only queried if lower-level name servers do not respond. They are central to linking domains and IP addresses and are coordinated by ICANN. There are 13 global root servers. |
| Authoritative Nameserver   | Authoritative name servers have definitive data for a specific zone, responding directly to queries within that zone. If unable to answer, the query escalates to the root server.  |
| Non-authoritative Nameserver | Non-authoritative name servers provide cached DNS response data from previous queries but do not hold data authority themselves.                                                  |
| Forwarding Server          | Forwarding servers only redirect DNS queries to another server for processing.                                                                                                     |
| Resolver                   | Resolvers handle DNS queries locally on a computer or router but are not authoritative for DNS zones.            

### DNS Records: 
| DNS Record | Description                                                                                   |
|------------|-----------------------------------------------------------------------------------------------|
| A          | Maps a domain to its corresponding IPv4 address.                                              |
| AAAA       | Maps a domain to its corresponding IPv6 address.                                              |
| MX         | Specifies the mail servers responsible for receiving email on behalf of a domain.             |
| NS         | Indicates the authoritative nameservers for the domain.                                        |
| TXT        | Contains varied information such as verification for Google Search Console and SSL certificates, along with SPF and DMARC records for email security. |
| CNAME      | Serves as an alias; e.g., linking multiple subdomains to the same IP address.                 |
| PTR        | Performs reverse DNS lookup, converting IP addresses back to domain names.                    |
| SOA        | Provides essential administrative information about a DNS zone, including the contact email.  |

### bind9 
- very often used dns server on linux 
- https://www.isc.org/bind/
- Doku: https://wiki.debian.org/Bind9
```
named.conf.local
named.conf.options
named.conf.log
```
It contains the associated RFC where we can customize the server to our needs and our domain structure with the individual zones for different domains. The configuration file named.conf is divided into several options that control the behavior of the name server. A distinction is made between global options and zone options.

Global options are general and affect all zones. A zone option only affects the zone to which it is assigned. Options not listed in named.conf have default values. If an option is both global and zone-specific, then the zone option takes precedence.

#### Local DNS Configuration
```sh
cat /etc/bind/named.conf.local
```
#### Zone Files
```sh
cat /etc/bind/db.domain.com

;
; BIND reverse data file for local loopback interface
;
$ORIGIN domain.com
$TTL 86400
@     IN     SOA    dns1.domain.com.     hostmaster.domain.com. (
                    2001062501 ; serial
                    21600      ; refresh after 6 hours
                    3600       ; retry after 1 hour
                    604800     ; expire after 1 week
                    86400 )    ; minimum TTL of 1 day

      IN     NS     ns1.domain.com.
      IN     NS     ns2.domain.com.

      IN     MX     10     mx.domain.com.
      IN     MX     20     mx2.domain.com.

             IN     A       10.129.14.5

server1      IN     A       10.129.14.5
server2      IN     A       10.129.14.7
ns1          IN     A       10.129.14.2
ns2          IN     A       10.129.14.3

ftp          IN     CNAME   server1
mx           IN     CNAME   server1
mx2          IN     CNAME   server2
www          IN     CNAME   server2
```
#### Reverse Name Resolution Zone Files
```sh 
cat /etc/bind/db.10.129.14

;
; BIND reverse data file for local loopback interface
;
$ORIGIN 14.129.10.in-addr.arpa
$TTL 86400
@     IN     SOA    dns1.domain.com.     hostmaster.domain.com. (
                    2001062501 ; serial
                    21600      ; refresh after 6 hours
                    3600       ; retry after 1 hour
                    604800     ; expire after 1 week
                    86400 )    ; minimum TTL of 1 day

      IN     NS     ns1.domain.com.
      IN     NS     ns2.domain.com.

5    IN     PTR    server1.domain.com.
7    IN     MX     mx.domain.com.
...SNIP...
```

#### Dangerous Settings
| Option          | Description                                                              |
|-----------------|--------------------------------------------------------------------------|
| allow-query     | Defines which hosts are allowed to send requests to the DNS server.      |
| allow-recursion | Defines which hosts are allowed to send recursive requests to the DNS server. |
| allow-transfer  | Defines which hosts are allowed to receive zone transfers from the DNS server. |
| zone-statistics | Collects statistical data of zones.                                      |

## Footprinting & Enumeration
### whois
```sh
whois 157.240.199.35
```
### nslookup
```sh
nslookup 
```
####  A Records
```sh
nslookup inlanefreight.com
```
#### A Records for a Subdomain
```sh
nslookup -query=A facebook.com
```
#### PTR Records for ip address
```sh
nslookup -query=PTR 134.209.24.248
```
#### Any Record
```sh
nslookup -query=ANY paypal.com
```
#### Txt Record
```sh
nslookup -query=TXT facebook.com
```
#### Identifying Nameservers
```sh
nslookup -type=NS zonetransfer.me
```

####  Testing for ANY and AXFR Zone Transfer
```sh
nslookup -type=any -query=AXFR zonetransfer.me nsztm1.digi.ninja
```


### Dig
#### Dig with setted nameserver
```sh
dig facebook.com @1.1.1.1

dig a www.facebook.com @1.1.1.1 #get a record

dig -x 31.13.92.36 @1.1.1.1 #get ptr record


```
#### DIG - SOA Query
```sh
dig soa www.inlanefreight.com #gives the start of authority record

; <<>> DiG 9.16.27-Debian <<>> soa www.inlanefreight.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15876
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.inlanefreight.com.         IN      SOA

;; AUTHORITY SECTION:
inlanefreight.com.      900     IN      SOA     ns-161.awsdns-20.com. awsdns-hostmaster.amazon.com. 1 7200 900 1209600 86400

;; Query time: 16 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Thu Jan 05 12:56:10 GMT 2023
;; MSG SIZE  rcvd: 128

The dot (.) is replaced by an at sign (@) in the email address. So admin email is awsdns-hostmaster@amazon.com.
```
#### DIG - NS Query
```sh
dig ns inlanefreight.htb @10.129.236.177 #gives the name servers

 <<>> DiG 9.16.1-Ubuntu <<>> ns inlanefreight.htb @10.129.14.128
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45010
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: ce4d8681b32abaea0100000061475f73842c401c391690c7 (good)
;; QUESTION SECTION:
;inlanefreight.htb.             IN      NS

;; ANSWER SECTION:
inlanefreight.htb.      604800  IN      NS      ns.inlanefreight.htb.

;; ADDITIONAL SECTION:
ns.inlanefreight.htb.   604800  IN      A       10.129.34.136

;; Query time: 0 msec
;; SERVER: 10.129.14.128#53(10.129.14.128)
;; WHEN: So Sep 19 18:04:03 CEST 2021
;; MSG SIZE  rcvd: 107

```

#### DIG - Version Query
```sh
dig CH TXT version.bind 10.129.120.85
```

#### DIG - ANY Query
```sh
dig any inlanefreight.htb @10.129.236.177
```
#### DIG - AXFR Zone Transfer
```sh
dig axfr inlanefreight.htb @10.129.236.177
```
#### DIG - AXFR Zone Transfer - Internal
```sh
dig axfr internal.inlanefreight.htb @10.129.236.177
```
ns.inlanefreight.htb
### Brute Force Subdomain 
- wordlist: https://github.com/danielmiessler/SecLists/blob/master/Discovery/DNS/subdomains-top1million-5000.txt
```sh
# Example 1
for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.inlanefreight.htb @10.129.236.177 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done

# Example 2: 
dnsenum --dnsserver 10.129.236.177 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb

dnsenum --dnsserver 10.129.236.177  --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/fierce-hostlist.txt inlanefreight.htb
# Example 3: 
sudo gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -u inlanefreight.htb
```
