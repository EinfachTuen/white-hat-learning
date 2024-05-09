# mysql
- port 3306

## Configuration
#### Default configuration
```sh
sudo apt install mysql-server -y
cat /etc/mysql/mysql.conf.d/mysqld.cnf | grep -v "#" | sed -r '/^\s*$/d'

    [client]
    port		= 3306
    socket		= /var/run/mysqld/mysqld.sock
    
    [mysqld_safe]
    pid-file	= /var/run/mysqld/mysqld.pid
    socket		= /var/run/mysqld/mysqld.sock
    nice		= 0
    
    [mysqld]
    skip-host-cache
    skip-name-resolve
    user		= mysql
    pid-file	= /var/run/mysqld/mysqld.pid
    socket		= /var/run/mysqld/mysqld.sock
    port		= 3306
    basedir		= /usr
    datadir		= /var/lib/mysql
    tmpdir		= /tmp
    lc-messages-dir	= /usr/share/mysql
    explicit_defaults_for_timestamp
    
    symbolic-links=0
    
    !includedir /etc/mysql/conf.d/
```
#### Dangerous Settings:
| Setting           | Description                                                                                         |
|-------------------|-----------------------------------------------------------------------------------------------------|
| user              | Sets which user the MySQL service will run as.                                                      |
| password          | Sets the password for the MySQL user.                                                               |
| admin_address     | The IP address on which to listen for TCP/IP connections on the administrative network interface.    |
| debug             | This variable indicates the current debugging settings.                                             |
| sql_warnings      | This variable controls whether single-row INSERT statements produce an information string if warnings occur. |
| secure_file_priv  | This variable is used to limit the effect of data import and export operations.                     |


## Commands
#### Connect to MySQL without password
```sh
mysql -h 10.129.108.116 -u root 
-h = hostshow
-u = user
```
#### Connect to MySQL with password
```sh
mysql -u robin -probin -h 10.129.108.116
```
#### SQL 
```
show databases; -- show databases
select version(); -- show version
use mysql; -- use database
show tables; -- show tables         
show columns from <table>;   -- Show all columns in the selected database
select * from host_summary;  -- select in table  
select * from <table> where <column> = "<string>";   -- Search for needed string in the desired table.             
```

## Enumeration / Footprinting
### Nmap
```sh
sudo nmap 10.129.108.116 -sV -sC -p3306 --script mysql*

```