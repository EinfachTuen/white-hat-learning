# Webshells

## about upload
Our goal is to upload the PHP web shell via the Vendor Logo browse button. Attempting  will maybe fail if the file type is wrong. If it only allow uploading image file types (.png,.jpg,.gif, etc.) for example.
We can often bypass this utilizing Burp Suite by setting another file type.
## Laudanum 
Laudanum is a repository of ready-made files that can be used to inject onto a victim
- https://github.com/jbarcia/Web-Shells/tree/master/laudanum
- in Kali and pwndbox saved in `/usr/share/webshells/laudanum`
- 
![laudanum-shell-aspx-setting.png](media%2Flaudanum-shell-aspx-setting.png)

## Antak Webshell
Antak is a web shell built-in ASP.Net included within the Nishang project. 
- https://github.com/samratashok/nishang
- preinstalled in kali and pwnbox saved in /usr/share/nishang/Antak-WebShell

Antak web shell functions like a Powershell Console. However, it will execute each command as a new process. It can also execute scripts in memory and encode commands you send. As a web shell, Antak is a pretty powerful tool.

### With Antak dont forget to set credentials
![Antak-shell-configure.png](media%2FAntak-shell-configure.png)

## PHP Web Shells
there are a lot different
- https://github.com/WhiteWinterWolf/wwwolf-php-webshell


## Considerations when Dealing with Web Shells

When using web shells during penetration testing, consider the following potential issues:
- **File Deletion**: Web applications might automatically delete files after a set period.
- **Limited Interactivity**: Navigating the file system, downloading/uploading files, and chaining commands (e.g., `whoami && hostname`) may not work, slowing down progress.
- **Instability**: Non-interactive web shells can be unstable.
- **Evidence**: Higher risk of leaving proof of the attack.
- **Stealth**: For evasive assessments, operate stealthily to help clients test their detection capabilities. Emulate malicious attacker methods, attempt to establish a reverse shell, and delete the payload after execution.
- **Documentation**: Document all methods and payloads used, noting what worked and what didn’t. Include file names, upload locations, and hashes (e.g., SHA1, MD5) in reports for attribution.
