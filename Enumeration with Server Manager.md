
Because servers are hardly ever logged on unless its for maintenance this gives you an easy way for enumeration only using the built in windows features such as the server manager. If you already have domain admin you have a lot of access to the server manager in order to change trusts, add or remove users, look at groups, this can be an entry point to find other users with other sensitive information on their machines or find other users on the domain network with access to other networks in order to pivot to another network and continue your testing.

The only way to access the server manager is to rdp into the server and access the server over an rdp connection

`remotedesktop -u Administrator -d CONTROLLER <10.10-ip->`

