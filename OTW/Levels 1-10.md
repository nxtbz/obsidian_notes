
export URL=bandit.labs.overthewire.org

Warning: Permanently added '[bandit.labs.overthewire.org]:2220' (ED25519) to the list of known hosts.
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

bandit0@bandit.labs.overthewire.org's password: 

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org


Welcome to OverTheWire!

If you find any problems, please report them to the #wargames channel on
discord or IRC.

--[ Playing the games ]--

  This machine might hold several wargames.
  If you are playing "somegame", then:

    * USERNAMES are somegame0, somegame1, ...
    * Most LEVELS are stored in /somegame/.
    * PASSWORDS for each level are stored in /etc/somegame_pass/.

  Write-access to homedirectories is disabled. It is advised to create a
  working directory with a hard-to-guess name in /tmp/.  You can use the
  command "mktemp -d" in order to generate a random and hard to guess
  directory in /tmp/.  Read-access to both /tmp/ is disabled and to /proc
  restricted so that users cannot snoop on eachother. Files and directories
  with easily guessable or short names will be periodically deleted! The /tmp
  directory is regularly wiped.
  Please play nice:

    * don't leave orphan processes running
    * don't leave exploit-files laying around
    * don't annoy other players
    * don't post passwords or spoilers
    * again, DONT POST SPOILERS!
      This includes writeups of your solution on your blog or website!

--[ Tips ]--

  This machine has a 64bit processor and many security-features enabled
  by default, although ASLR has been switched off.  The following
  compiler flags might be interesting:

    -m32                    compile for 32bit
    -fno-stack-protector    disable ProPolice
    -Wl,-z,norelro          disable relro

  In addition, the execstack tool can be used to flag the stack as
  executable on ELF binaries.

  Finally, network-access is limited for most levels by a local
  firewall.

--[ Tools ]--

 For your convenience we have installed a few useful tools which you can find
 in the following locations:

    * gef (https://github.com/hugsy/gef) in /opt/gef/
    * pwndbg (https://github.com/pwndbg/pwndbg) in /opt/pwndbg/
    * peda (https://github.com/longld/peda.git) in /opt/peda/
    * gdbinit (https://github.com/gdbinit/Gdbinit) in /opt/gdbinit/
    * pwntools (https://github.com/Gallopsled/pwntools)
    * radare2 (http://www.radare.org/)

 Both python2 and python3 are installed.

--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us on discord or IRC.

  Enjoy your stay!


# Level 0-1 
login with ssh with the given username and pwd.
`ssh bandit0@<url> -p 2220` 

password for level1 is in the readme
`cat readme`

```
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

##### level 1
To find the password for level 2
After login `ssh bandit1@... -p2220` we can prompt and see around with `ls`.
All we see is `-` also known as a 'dashed filename'  

##### Level 2
Filename with spaces
`cat *` aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG



##### Level 3 
Hidden files 
`ls -la` & `cat .hidden` 

##### Level 4
Only Human Readeble files

there are multiple ways to go at it, but you want to scan the map, or its contents for a file that is 'human readable', again, the files have a 'dashed' naming convention, which makes outputting it with `cat` just a little bit cumbersume. 

Let's scan for human readable files
`file -- *` or `file . -size 1033c` 

turns out `-file07` is ASCII text, so with `cat ./-file07` we will get the password.

##### Level 5
another find, but more dir's and files this time. 
`file <dir> -size <x> ! -executable -exec file {} + ` will go a little deeper and will ingore executables and such.

##### Level 6
Find entireserver, user, group, filesize  
`file / -user bandit6 -group bandit7 -size 33c` 
  
##### Level8 
The password for the next level is stored in the file **data.txt** next to the word **millionth**
`find data.txt`
`cat data.txt | grep milionth`


##### Level9
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

```
sort data.txt | uniq -u 
```

#### level10
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

```
string data.txt | grep ===
```


#### level 11

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data
```
man base64 
cat data.txt | base64 -d 
#or
base64 -d data.txt
```

#### level 12
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

```
<tr> 
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
>the password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

#### level 13

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

(warning, rabbit hole)

```
# first outout data Hexfile BACK (reverse) to 'a' datafile
cat data.txt | xxd -r > data

# turns out the data file is from another 'type'
file data
>data: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix


# rename the file to data2.gz, and unzip
mv data2.bin data2.gz
gzip -d data2.gz

# and this rabbit hole continues for 10x times

mv data3 data4.gz  
gzip -d data4.gz  

file data4  
>data4: POSIX tar archive (...

mv data4 data5.tar  
tar -xf data5.tar  
tar -xf data6.tar  
bzip2 -d data7.bz  
tar -xf data8.tar  
mv data8.bin data9.gz  
gzip -d data9.gz  

file data9  
>data9: ASCII textbandit12@bandit:/tmp/secttp$ 

cat data9  
>The password is ==**8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL**==

```



#### level 14

The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on


```
quite easy one, 
ls -la 
> ssh_keyfile.private

$ ssh bandit14@localhost -p 2220 -i ssh_keyfile.private 
>bandit14@locahost: 
$ cat /etc/bandit_password/bandit14.txt
```


#### level 14

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

```
# nmap localhost, port 3000 has a secure backup service or something
Not shown: 993 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
1111/tcp  open  lmsocialserver
1840/tcp  open  netopia-vo2
4321/tcp  open  rwhois
8000/tcp  open  http-alt
8888/tcp  open  sun-answerbook
30000/tcp open  ndmps

#quick google says we can use netcat to pipe a string into it
$ echo "<the previous password" | nc localhost 30000
>Correct!
>jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt



```

#### level 15

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.

**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**



Have to say the hints and doc's didn't gave much answers, had to google this one. 
but in laymens words, you use the openssl program to adopt the s_client for testing. 
You want it to connect to the localhost at a certain port, and use the -flag's given by the hints.
```
# this one is sketchy

$echo "<old_password>" | openssl s_client -connect 127.0.0.1:30001 -ign_eof
>... JQttfApK4SeyHwDlI9SXGR50qclOAil1



# same can be achieved by silencing the output 2>1
$echo "<old_password>" | openssl s_client -connect 127.0.0.1:30001 -ign_eof
```



#### level 16

The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Finding out the ports:
```
bandit16@bandit:~$ nmap --script ssl-enum-ciphers 127.0.0.1 -p 31000-32000
```

results where two port potentialy responding to tsl
let's hit the last one with our credentials from current level

```
bandit16@bandit:~$ echo "JQttfApK4SeyHwDlI9SXGR50qclOAil1" | openssl s_client -connect 127.0.0.1:31790 -ign_eof

> read R BLOCK
	Correct!
	-----BEGIN RSA PRIVATE KEY-----
	MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
	imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
	Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
	DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
	JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
	x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
	KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
	J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
	d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
	YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
	vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
	+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
	8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
	SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
	HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
	SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
	R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
	Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
	R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
	L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
	blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
	YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
	77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
	dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
	vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
	-----END RSA PRIVATE KEY-----



```




#### level 17

There are 2 files in the homedirectory: **passwords.old and passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**

```
bandit17@bandit:~$ diff passwords.new passwords.old 
42c42
< hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
---
> glZreTEH1V3cGKL6g4conYqZqaEj0mte

```




#### level 18

The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

`ssh user@level "cat readme"`
awhqfNnAbc1naukrpqDYcF95h7HoMTrC



#### level 19



#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11

bandit19: awhqfNnAbc1naukrpqDYcF95h7HoMTrC
bandit18: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
bandit17 >keyfile< 
bandit16 JQttfApK4SeyHwDlI9SXGR50qclOAil1
bandit15 jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
bandit14 fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
bandit13 wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
bandit12 JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
bandit11 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
bandit10 G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
bandit9 EN632PlfYiZbn3PhVK3XOGSlNInNE00t
bandit8 TESKZC0XvTetK0S9xNwm25STk5iWrBvP
bandit7 z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
bandit6 P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
