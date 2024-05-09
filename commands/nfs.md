## Network File System (NFS)
- allows remote access to files over a network
- open standard anybody can implement
- linux und unix
- can not communicate directly with smb
- https://en.wikipedia.org/wiki/Network_File_System
- port 2049 usually used
- or port 111 RPC
- nfs is based on rpc authentication is shifted on protokoll 
### Versions 
- NFSv2	It is older but is supported by many systems and was initially operated entirely over UDP.
- NFSv3	It has more features, including variable file size and better error reporting, but is not fully compatible with NFSv2 clients.
- NFSv4	It includes Kerberos, works through firewalls and on the Internet, no longer requires portmappers, supports ACLs, applies state-based operations, and provides performance improvements and high security. It is also the first version to have a stateful protocol.

### Configuration: 
```shell
cat /etc/export #contains a table of physical filesystems
# /etc/exports: the access control list for filesystems which may be exported
#               to NFS clients.  See exports(5).
#
# Example for NFSv2 and NFSv3:
# /srv/homes       hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
#
# Example for NFSv4:
# /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
# /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
```
### Create one: 
- shares the folder /mnt/nfs to the subnet 10.129.14.0/24 
- This means that all hosts on the network will be able to mount this NFS share
```shell
root@nfs:~# echo '/mnt/nfs  10.129.14.0/24(sync,no_subtree_check)' >> /etc/exports
root@nfs:~# systemctl restart nfs-kernel-server 
root@nfs:~# exportfs

/mnt/nfs      	10.129.14.0/24
```

### Mounting
```shell
mount -t nfs <target-ip>:/<share> <mount-point>
# mount point is where the share should be mounted to
# Example 1
sudo mount -t nfs 10.129.188.20:/var/nfs /home/htb-ac-1245260/nfs
sudo mount -t nfs 10.129.188.20:/mnt/nfsshare /home/htb-ac-1245260/nfsshare

# Example 2
mkdir target-NFS
sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
cd target-NFS
tree .
```

### Unmounting
```shell
umount /mnt/nfs
```
 
### List Contents

```shell
ls -l mnt/nfs/ #List Contents with Usernames & Group Names
```
```shell
ls -n mnt/nfs/ #List Contents with User IDs & Group IDs
```
## Enumerationg and Foodprinting 
- if found we can try to mount, see above
### nmap: 
```shell
sudo nmap 10.129.188.20  -p111,2049 -sV -sC

sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049 
```
### Show Available NFS Shares
```shell
showmount -e 10.129.188.20
```
### with RPCinfo
```shell
rpcinfo -p <target-ip>
```

