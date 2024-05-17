# Nessus

- download https://www.tenable.com/downloads/nessus?loginAttempted=true
- register https://www.tenable.com/products/nessus/activation-code (Essential for Free)


#### Installation after download of course

```sh
dpkg -i Nessus-8.15.1-ubuntu910_amd64.deb

```
#### Starting

```sh
sudo systemctl start nessusd.service
```
- open https://localhost:8834

- follow installation steps
- Essential is the free version

#### Scan Type descriptions
- https://docs.tenable.com/nessus/Content/ScanAndPolicyTemplates.htm

#### measure network impact of vulnerability scanning:
```sh
sudo apt install vnstat
sudo vnstat -l -i eth0
```