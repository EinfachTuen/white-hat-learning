## Photon Lockdown
ve located the adversary's location and must now secure access to their Optical Network Terminal to disable their internet connection. 
Fortunately, we've obtained a copy of the device's firmware, which is suspected to contain hardcoded credentials. 
Can you extract the password from it?

```shell
file rootfs ## resulSquashfs filesystem, little endian, version 4.0, zlib compressed,t 
unsquashfs rootfs
grep -ri "3.0.5" /squashfs-root #to much results
#searched a long long time ... 
la # found almost there in /home/.41fr3d0
#got a tip its  called with "HTB{...}"
#so that worked
grep --include=*.{txt,conf,xml,php} -rnw '.' -e 'HTB' 2>/dev/null
```