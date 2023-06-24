

######
read _>  https://linuxhint.com/special-permissions-suid-guid-sticky-bit/
######



Take a look at the following demonstration of how maximum privileges (rwx-rwx-rwx) look:

r = read
w = write
x = execute  

    **user**     **group**     **others**  
    rwx       rwx       rwx  
    421       421       421

The maximum number of bit that can be used to set permission for each user is 7, which is a combination of read (4) write (2) and execute (1) operation. 

Thus, if you set permissions using **"chmod"** as **755**, then it will be: rwxr-xr-x.

`When extra bit **“4”** is set to user(Owner) it becomes **SUID** (Set user ID) and when bit **“2”** is set to group it becomes **SGID** (Set Group ID).
`



But when special permission is given to each user it becomes SUID or SGID. When extra bit **“4”** is set to user(Owner) it becomes **SUID** (Set user ID) and when bit **“2”** is set to group it becomes **SGID** (Set Group ID).  

Therefore, the permissions to look for when looking for SUID is:

SUID:
rws-rwx-rwx

GUID:
rwx-rws-rwx


**Finding SUID Binaries**  

if we want to do this manually we can use the command: 
` find / -perm -u=s -type f 2>/dev/null `


**Find** - Initiates the "find" command  

**/** - Searches the whole file system  
**-perm** - searches for files with specific permissions  
**-u=s** - Any of the permission bits _mode_ are set for the file. Symbolic modes are accepted in this form
**-type f** - Only search for files  
**2>/dev/null** - Suppresses errors




# to get all the suids  
  
find / -perm -4000 2> /dev/null  
  
# to get all the guids  
  
find / -perm -2000 2> /dev/null  
  
# find all sticky bits  
  
find / -perm -1000 2> /dev/null