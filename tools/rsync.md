# Rsync
- https://linux.die.net/man/1/rsync
- Rsync is a fast and efficient tool for locally and remotely copying files. It can be used to copy files locally on a given machine and to/from remote hosts. 
- Rsync over SSH guide: https://phoenixnap.com/kb/how-to-rsync-over-ssh

## Footprinting
### Scanning for Rsync
```sh
sudo nmap -sV -p 873 127.0.0.1
```
### Probing for Accessible Shares
```sh
nc -nv 127.0.0.1 873
```
### Enumerating an Open Share
```sh
rsync -av --list-only rsync://127.0.0.1/dev
```
#### sync to attack host:
```sh
rsync -av rsync://127.0.0.1/dev
```
- -e ssh flag to transfer orver rsync over ssh
- or -e "ssh -p2222" if a non-standard port is in use for SSH
- 