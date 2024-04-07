## SQL Injections
SQL Injections are a type of attack that allows an attacker to execute arbitrary SQL code on a database. 

### Tipps to find SQL Injections
- Scan host for vulnerabilites
- Identify webserver and web application
- Identify software and version if possible
- Search for vulnerabilities in the software (Exploit DB, Searchsploit)
- Use SQLmap to automate the process
- Test everything that could be vulnerable (Parameters, Forms, Cookies, Headers and more)
- Test different kind of injection pattern
- Its possible that the SQL Injection don't give a verbose error messages

### How to find manually
- " ' " powerful tool 
- " ' or 1=1 -- -" 
- "or 1=1 -- -" 
- " ' or 1=2 -- -" if 1=1 doesnt work
- "or 1=2 -- -" if 1=1 doesnt work

For more manual enumartion see this guides:
- mini guide: https://www.exploit-db.com/papers/13650
- authentication bypass: https://pentestlab.blog/2012/12/24/sql-injection-authentication-bypass-cheat-sheet/


### SQLmap
Use SQLmap for automatically find SQL Injections. SQLmap is a powerful tool that can automate the process of finding and exploiting SQL Injections.