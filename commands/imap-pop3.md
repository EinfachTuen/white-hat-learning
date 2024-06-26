## IMAP / POP3
- port 143 (IMAP) or 993 (IMAPS) etc.
- port 110 (POP3) or 995 (POP3S) etc.


### Configuration

#### IMAP Commands
| Command              | Description                                                                                     |
|----------------------|-------------------------------------------------------------------------------------------------|
| 1 LOGIN username password | User's login.                                                                  |
| 1 LIST "" *          | Lists all directories.                                                                          |
| 1 CREATE "INBOX"     | Creates a mailbox with a specified name.                                                        |
| 1 DELETE "INBOX"     | Deletes a mailbox.                                                                              |
| 1 RENAME "ToRead" "Important" | Renames a mailbox.                                                                  |
| 1 LSUB "" *          | Returns a subset of names from the set of names that the User has declared as being active or subscribed. |
| 1 SELECT INBOX       | Selects a mailbox so that messages in the mailbox can be accessed.                             |
| 1 UNSELECT INBOX     | Exits the selected mailbox.                                                                     |
| 1 FETCH <ID> all     | Retrieves data associated with a message in the mailbox.                                       |
|1 FETCH 1 BODY[] | Fetches the body of the first email. |
| 1 CLOSE              | Removes all messages with the Deleted flag set.                                                |
| 1 LOGOUT             | Closes the connection with the IMAP server.                                                    |



#### POP3 Commands
| Command  | Description                                                               |
|----------|---------------------------------------------------------------------------|
| USER username | Identifies the user.                                                  |
| PASS password | Authentication of the user using its password.                        |
| STAT     | Requests the number of saved emails from the server.                      |
| LIST     | Requests from the server the number and size of all emails.               |
| RETR id  | Requests the server to deliver the requested email by ID.                 |
| DELE id  | Requests the server to delete the requested email by ID.                  |
| CAPA     | Requests the server to display the server capabilities.                   |
| RSET     | Requests the server to reset the transmitted information.                 |
| QUIT     | Closes the connection with the POP3 server.                               |


#### Dangerous Settings
| Setting                  | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| auth_debug               | Enables all authentication debug logging.                                   |
| auth_debug_passwords     | This setting adjusts log verbosity, the submitted passwords, and the scheme gets logged. |
| auth_verbose             | Logs unsuccessful authentication attempts and their reasons.                |
| auth_verbose_passwords   | Passwords used for authentication are logged and can also be truncated.     |
| auth_anonymous_username  | This specifies the username to be used when logging in with the ANONYMOUS SASL mechanism. |

### nmap:
```sh
sudo nmap 10.129.154.138 -sV -p110,143,993,995 -sC
```

### cURL
```sh
curl -k 'imaps://10.129.154.138' --user user:p4ssw0rd -v 
```
### OpenSSL

#### TLS Encrypted Interaction POP3
```sh
openssl s_client -connect 10.129.154.138:pop3s
```
#### TLS Encrypted Interaction IMAP
```sh
openssl s_client -connect 10.129.154.138:imaps
```

### ncat
#### POP3
```sh
ncat 10.129.154.138 110
```

#### IMAP
```sh
ncat 10.129.154.138 143
```