## BEEF Framework
BeEF is short for The Browser Exploitation Framework. It is a penetration testing tool that focuses on the web browser. Leveraging client-side attack vectors, BeEF allows penetration testers to assess the security of a target by using the web browser as a pivot point. BeEF is a powerful tool that can be used to exploit web browsers and gather information from them. It is a great tool for testing the security of web applications and web browsers. BeEF is a part of the Kali Linux distribution and is also available as a standalone tool.
- can hook browsers
- can capture keystrokes
- can create dialogs etc.
- very detailed logs what the user is doing

### Usage
#### Example
```sh
nmap -sV <target-ip> #scan a target found ability mail server 2013
#1
searchsploit ability mail server 2013 # Result is a persistent cross-site scripting vulnerability
#Search for it in exploit db and understand and modifiy it, add correct ip for the hook to beef
#2. Start BeEF
#3 Send exploit in this case its a mail send to the user if he open it in ability mail server, the XSS vulnerability is used to hook him
```
