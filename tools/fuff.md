# Fuff
A fast web fuzzer written in Go.
- https://github.com/ffuf/ffuf

## Options 
```
MATCHER OPTIONS:
  -mc                 Match HTTP status codes, or "all" for everything. (default: 200,204,301,302,307,401,403,405)
  -ml                 Match amount of lines in response
  -mr                 Match regexp
  -ms                 Match HTTP response size
  -mw                 Match amount of words in response

FILTER OPTIONS:
  -fc                 Filter HTTP status codes from response. Comma separated list of codes and ranges
  -fl                 Filter by amount of lines in response. Comma separated list of line counts and ranges
  -fr                 Filter regexp
  -fs                 Filter HTTP response size. Comma separated list of sizes and ranges
  -fw                 Filter by amount of words in response. Comma separated list of word counts and ranges
  
-w: Path to our wordlist
-u: URL we want to fuzz
-H "HOST: FUZZ.randomtarget.com": This is the HOST Header, and the word FUZZ will be used as the fuzzing point.
-fs 612: Filter responses with a size of 612, default response size in this case.
-rate 100: Set the rate of requests per second. Default is 100.
--recursion: Activates the recursive scan.
--recursion-depth: Specifies the maximum depth to scan.
```
## Usage with host header 
### Custom wordlist
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
ffuf -w ./vhosts -u http://10.129.42.195 -H "HOST: FUZZ.inlanefreight.htb" -fs 612
```
### Existing wordlist
```shell
ffuf -w /opt/useful/SecLists/Discovery/DNS/namelist.txt -u http://192.168.10.10 -H "HOST: FUZZ.inlanefreight.htb" -fs 612
# -w: Path to our wordlist
# -u: URL we want to fuzz
# -H "HOST: FUZZ.randomtarget.com": This is the HOST Header, and the word FUZZ will be used as the fuzzing point.
# -fs 612: Filter responses with a size of 612, default response size in this case.
```

## Spidering
```shell
ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt
# -recursion: Activates the recursive scan.
# -recursion-depth: Specifies the maximum depth to scan.
# -u: Our target URL, and FUZZ will be the injection point.
# -w: Path to our wordlist.
```

## Sensitive Information Disclosure
- wordlist: raft-[ small | medium | large ]-extensions.txt can be used to find sensitive information disclosure.
- https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/

#### example Fuff cmd  to search for sensitive information disclosure
```shell 
ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://192.168.10.10/FOLDERS/WORDLISTEXTENSIONS
```

### Extract words from a website: 
cewl -m5 --lowercase -w wordlist.txt http://192.168.10.10