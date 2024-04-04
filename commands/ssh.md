## SSH

### SSH Tunneling:

```bash

ssh -L 1234:localhost:22 user@remote.example.com
```

n the scenario we are currently facing, we want to forward traffic from any given local port, for instance
1234 , to the port on which PostgreSQL is listening, namely 5432 , on the remote server. We therefore
specify port 1234 to the left of localhost , and 5432 to the right, indicating the target port.
```bash
ssh -L 1234:localhost:5432 christine@10.129.228.195
```