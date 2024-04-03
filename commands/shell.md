
echo to host file
```sh
echo "10.129.152.215 unika.htb" | sudo tee -a /etc/hosts
```

liste aller offenen Ports
```sh
sudo netstat -tulnp
```