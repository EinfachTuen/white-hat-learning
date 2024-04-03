## SMB

### SMB Responder: 

-I choose network interface (In the context of Responder, 

```sh
git clone https://github.com/lgandx/Responder
```
Verify that the Responder.conf is set to listen for SMB requests.

edit resolver conf if necessary

```sh
cat Responder.conf
```
```
sudo python3 Responder.py -I tun0

Specifying -I tun0 means that Responder will listen for network requests coming through the tun0 interface. 
This could be useful if you're running Responder on a system that's connected to a VPN, 
and you want Responder to only interact with network traffic that's coming over the VPN connection.)

```
server is now listening

