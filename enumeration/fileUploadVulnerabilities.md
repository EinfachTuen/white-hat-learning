## FileUpload Vulnerabilities
File upload vulnerabilities in web apps allow server-executable uploads, enabling various attacks.
- Page allows user to upload files to the server
- if not properly secured, attacker can upload malicious files
- its helpful to identify the programming language and the server type
- usually executables and scripts are not allowed to be uploaded but sometimes it is possible to bypass this check


### FileChanges that can trick the server
- things like php3,php5, PhP, phtml insteadof php 
- asp, aspx for asp
- pl, pm, cgi, ib for perl
- jsp,jspx, jsw, jsv, jspf for java
- Try all of this with different large and small letters
- change mimetypes cause some server only check mime types
- try to upload a file with a double extension like .php.jpg
- combine Code for example PHP within a JPG but the ending is php but if it checks magic bytes it maybe fall for it
