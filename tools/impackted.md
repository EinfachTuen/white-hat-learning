## Impacket 

creates a remote service by uploading a randomly-named executable on the ADMIN$ share on the
remote system and then register it as a Windows service.This will result in having an interactive shell
available on the remote Windows system via TCP port 445 .


Psexec requires credentials for a user with local administrator privileges or higher since reading/writing to
the ADMIN$ share is required. Once you successfully authenticate, it will drop you into a NT
AUTHORITY\SYSTEM shell.

We can Download Impacket from this link.
Installation guide:

Note: In case you don't have pip3 (pip for Python3) installed, or Python3, install it with the following commands:
```sh
sudo apt install python3 python3-pip
```
The pkexec utility can be found at /impacket/examples/pkexec.py . Run the following command to see
the help information for psexec.py :
```sh
psexec.py -h
```