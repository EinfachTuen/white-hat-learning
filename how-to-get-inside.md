## How to get inside:

### Web Edition:

1.) run Nmap on server

2.) when http found try to open website

2a.) Websites redirect, this can be named based virtual hosting

2a1.) add the ip to /etc/hosts

2.b) Search if there are other host somewhere in the website like for example: mail@thetoppers.htb

2.c) scan for subdomains if possible with all hosts

2.d) If subdomain found add to hosts as well

2.e) if nmap delivers Did not follow redirect to http://ignition.htb
```
In short, multiple websites can share the same IP address, allowing users to access them separately by
visiting the specific hostnames of each website instead of the hosting server's IP address. The webserver we
are making requests to is throwing us an error because we haven't specified a certain hostname out of the
ones that could be hosted on that same target IP address. From here, we'd think that simply inputting
ignition.htb instead of the target IP address into the search bar would solve our issue, but unfortunately,
this is not the case. When entering a hostname instead of an IP address as the request's destination, there is
a middleman involved that you might not know about.
```

3.) run gobuster with a suifficient wordlist to find hidden directories

3a.) If a url parameter is found, try to inject a file

4.) if login is present try standard credentials:

```
    admin:admin
    guest:guest
    user:user
    root:root
    administrator:password
```

5.) try sql injection