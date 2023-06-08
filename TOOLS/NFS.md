 
NFS-COMMON

1; port scan 
`nmap -A -p- -T4 10.10.205.206`

2: showmount
Use showmount to list the available shares
`showmount -e <ip>`



3: mount
Create a folder and mount the share
`sudo mount -t nfs IP:share /tmp/mount/ -nolock`

so in this case should be: 
`sudo mount -t nfs 10.10.205.254/home /tmp/mount -nolock`

 
	mount : Execute the mount command
	-t nfs : Type of device to mount, then specifying that it's NFS
	IP:share  : The IP Address of the NFS server, and the name of the share we wish to mount
	-nolock : Specifies not to use NLM locking

