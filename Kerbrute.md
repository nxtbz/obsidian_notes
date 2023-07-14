
By brute-forcing Kerberos pre-authentication, you do not trigger the account failed to log on event which can throw up red flags to blue teams. When brute-forcing through Kerberos you can brute-force by only sending a single UDP frame to the KDC allowing you to enumerate the users on the domain from a wordlist.

`./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt` 
This will brute force user accounts from a domain controller using a supplied wordlist
