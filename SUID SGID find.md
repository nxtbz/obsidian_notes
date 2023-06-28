In Linux, SUID (**set owner userId upon execution**) is a particular type of file permission given to a file. SUID gives temporary permissions to a user to run the program/file with the permission of the file owner (rather than the user who runs it).  

For example, the binary file to change your password has the SUID bit set on it (/usr/bin/passwd). This is because to change your password; it will need to write to the shadowers file that you do not have access to, root does; so it has root privileges to make the right changes.

`find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null`

find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null

find / -user root -perm -4000 -exec ls -ldb {} \;


