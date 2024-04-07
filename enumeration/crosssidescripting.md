### XSS / Cross Site Scripting
XSS is a vulnerability that allows an attacker to inject malicious code into a web application.
- Client side injection attack
- Happens typically when user input is not sanitized
- Three Types:
  - Stored XSS
  - Reflected XSS
  - DOM Based XSS,
- JavaScript, HTML, *VBScript, ActiveX, Flash or any other code that the browser can execute.*


### Reflected XSS
- The attacker sends a link to the victim
- redirect to the attackers controlled page
- its possible ot insert malicious code into the page

### Stored XSS
- Served to all users that can access the page
- often on forums, comments, chat, etc.
- often used to steal session cookies and login with them
- can also be used to deface a website

### DOM Based XSS
(Have to further read to fully understand)
- occures in the DOM
- difficult to detect
- can depend on the browser for execution