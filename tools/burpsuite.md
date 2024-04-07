## Burpsuite
made by portswigger [burpsuite](https://portswigger.net/burp)
- Tutorial LAbs: https://portswigger.net/web-security/all-labs
- Commuity edition is free
- For Professional Use Cases, buy pro version!
- Spidering Feature removed in version 2. But available in 1.7
- Install Burp CA can be found at http://burpsuite
- Burp generates own TLS

### Burp Suite Proxy
- has embedded browser
  - in Kali maybe not opening browser, fix with options-> misc-> "allow embedded browser" run in sandbox
- intercept is on by default
- can modify packets before sent
- can send requests to other burp suite tools

### Burp Suite Repeater
- can send http versions
- time based sql injection
- easily analyze requests

### Burp Suite Intruder
- in commuity throttled maybe use hydra instead of free
- brute force logins
- can grep
- can use payloads
#### Payloads:
- Sniper: attack one by one
- Battering Ram: attack all at once
- Pitchfork: uses one set of payloads on one position and another set on another position
- Cluster Bomb: uses all payloads on all positions

### Burp Suite Decoder
- can encode and decode
- different encodings
    - URL
    - Base64
    - Hex
    - ASCII Hex
    - HTML
    - Octal
    - Binary
    - GZIP

