# METASPLOIT 

## Portscan
`nmap -sS <ip>`

## udp_sweep
User Datagram Protocol, scan for users 

## smb_enumshares
See what shares there are on the ip

## smb_version
see what version software smb there is 


Run NMAP and store it in de db
`db_nmap -sV -p- 10.10.12.229`


The `hosts -h` and `services -h` commands can help you become more familiar with available options. 

Once the host information is stored in the database, you can use the `hosts -R` command to add this value to the RHOSTS parameter.

The `services` command used with the -S parameter will allow you to search for specific services in the environment. 


# walktrough
run over the target and lists ports and services 
`nmap -p- -sS -A <ip>`  

Go over specific port running a script for OS discovery of the file system service
`nmap 10.10.121.21 -p 443 — script smb-os-discovery`

Go over two ports, running vulnerability scripts 
`nmap 10.10.121.21 -p 139,445 — script vuln`





