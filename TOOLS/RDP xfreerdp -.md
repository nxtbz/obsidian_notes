Remote desktop 

When you have a user with system previleges you can easily add new users / groups
in cmd:
``
`net local <username> <password> /add`
eg
`net local god foobar /add`

and add god to the administrators 
`net localgroup administrators god /add`


```
`xfreerdp /dynamic-resolution +clipboard /cert:ignore /v:10.10.22.52 /u:Administrator /p:'TryH4ckM3!'`
